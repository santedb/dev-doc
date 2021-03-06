# Master Data Storage

The Master Data Management plugin permits your SanteDB CDR instance to store multiple copies of a single record based on the source system which provided the data. The MDM services are available on the following resources:

* Patient
* Place
* Provider
* Materials \(and Manufactured Materials\)
* Device Entities
* Persons

{% hint style="info" %}
The use of Master Data Management services require a compatible [Matching and Merge](../../extending-santedb/server-plugins/service-definitions/matching-merging-services/) service to operate. This is how the MDM solution detects candidate master records.
{% endhint %}

## MDM Data Storage Pattern

Within the data storage persistence layer, the MDM plugin will update/create locals using whatever underlying class was sent from the caller. Each caller is provided a complete copy of the record which they can update/edit.

The MDM plugin then determines:

* Is there a MASTER record which the IRecordMatching service has identified as positive match?
* Is the configuration enabled to automatically link these records?

If no MASTER is found, or the configuration does not permit auto-linking then a new MASTER of the base type is constructed \(Entity in case of Patient, Place, Material, etc. or Act in the case of Administration, Procedure, Observation, etc.\) and links the LOCAL record to this newly created master instance using the relationship type `MDM-MasterRecord`.



![](../../../.gitbook/assets/image%20%28179%29.png)

The master record should have **no data** associated with it. It is merely an anchor which is used to collect the local records. Typically a master record can have extensions, notes, identifiers, names, etc. associated with it, however these attributes should apply to the anchor point rather than for establishing ROT data.

### Candidate Links

In the case where a match between a LOCAL and MASTER record is ambiguous \(i.e. does is a Probable match or when Auto-Link is disabled\) the link between records is considered a candidate and the local is related to the MASTERs which it is a candidate for using the `MDM-CandidateLocal` relationship type.

In the scenario below, Good Health Clinic has registered John Doe born Jan 1 1980 with ID 1230493. The MDM layer has constructed a master record. A subsequent registration by HIV Health Clinic for John Doe, born sometime in 1980 with ID 3029402 as registered after.

Assuming that the match configuration was setup such that the HIV record had a match score below "DEFINITE" match, the MDM plugin would establish a new MASTER which contains one LOCAL. That LOCAL would also be related to the MASTER from Good Health Clinic with relationship type `MDM-CandidateLocal`.  


![](../../../.gitbook/assets/image%20%28186%29.png)

This candidate link exists until:

* A subsequent update from either the HIV Health Clinic \(to record 3029402\) or Good Health Clinic \(to record 1230493\) means that the patients no longer meet threshold for match.
* The match configuration is updated, which scores the link below the threshold for probable match.
* An administrator establishes a new link between the HIV Clinic and the MASTER of `MDM-IgnoreCandidate` \(which indicates a known false-match\).
* An administrator manually indicates that the HIV Health Clinic record is a known match to the MASTER \(in which case the MDM-MasterRecord link is removed and updated \(as shown below\).

![](../../../.gitbook/assets/image%20%28184%29.png)

### Record of Truth

The MDM solution permits the establishing of a Record Of Truth \(ROT\). The Record Of Truth is a new local instance which belongs to the SYSTEM and can only be updated when the security principal is permitted MDM Record Of Truth. 

A ROT record is a special pointer at a LOCAL whereby the LOCAL points to the MASTER record, and the MASTER points at the ROT with relationship type of `MDM-RecordOfTruth`. 

{% hint style="info" %}
It is possible to manually elevate an existing LOCAL as a ROT record, however this is not yet supported on user interfaces available.
{% endhint %}

![](../../../.gitbook/assets/image%20%28182%29.png)



### Privacy Masking

It is a commonly asked how the solution operates when a sensitive LOCAL record is shared with common health infrastructure. In the case of SanteDB's iCDR, when a MASTER record has multiple LOCALS the information returned to a caller is a synthesized copy of data within the LOCAL records.

The synthetization process uses a most-restrictive policy enforcement mechanism before considering a local for inclusion in the result. In the example illustrated above, the information sourced from the HIV Health Clinic is tagged as TABOO information. 

When a caller asks the CDR for the MASTER, the MDM service will call the `IPolicyDecisionService` and ask for a decision on each of the flagged policies in each of the locals and will return either:

* The UNION of data from both Good Health Clinic and HIV Health Clinic when TABOO has a **GRANT**, or
* Only data from Good Health Clinic when TABOO policy outcome is **DENY**, or
* Only the data from Good Health Clinic and an indicator of elevation required \(i.e. indicator more data is present\) when the TABOO policy outcome is **ELEVATE.**

\*\*\*\*

## MDM Service Relationships

The MdmDataManagementService should be configured in your application context. Upon start, this daemon will read the contents of the `ResourceMergeConfigurationSection` to determine the appropriate instances of `MdmResourceListener<T>` to construct and register with the provider.

![](../../../.gitbook/assets/image%20%28185%29.png)

For example, given a configuration as provided below

```markup
<section xsi:type="ResourceMergeConfigurationSection">
  <resources>
    <add type="Patient" matchConfiguration="org.santedb.smpi.matching.default" autoMerge="false" />
    <add type="Place" matchConfiguration="org.santedb.shfr.matching.default" autoMerge="false" />
  </resources>
</section>
```

The MdmDataManagementService on start would register two resource listeners for Patient and Place. It would furthermore, instruct each resource listener to use the specified match configuration for detecting candidate local&lt;&gt;master linkages.

### MDM Resource Listener

The resource listener instances created by the data management service subscribe to the repository events for the indicated type. The resource listener receives an event broadcast from the repository service whenever an event occurs and takes appropriate actions.

#### Data Update Operations

The `Saving` and `Inserting` events of the repository service are subscribed on service start. Whenever data through a repository is being actioned the events are raised and the following actions occur on the MDM Resource Listener:

* The instances are validated through OnPrePersistenceValidate\(\) method. Here the process ensures:
  * The caller is not attempting to update a MASTER record. If it is, the appropriate LOCAL for that principal is exchanged.
  * If the caller is attempting to create a RECORD OF TRUTH , it has appropriate permission to do so
* The Saving\(\) and Inserting\(\) event handlers are called next. These methods:
  * Call the matching service and attempt to establish whether the LOCAL is a candidate for an existing record
  * Appropriately obsolete/create resource links between the objects.
  * Cancels the caller \(i.e. overwrites the default call path\)
  * Returns a BUNDLE which is treated as a transaction on the persistence layer.

#### Data Query / Retrieval Operations

When a repository's `Find()` or `Get()` methods are called the repository will call the `Retrieving` and `Querying` event handlers. The MDM resource listener for that repository will perform the following operations:

* Cancel the default path of the repository
* Re-write the HDSI expression tree to query attributes related to the ROT or a LOCAL

The resource listener also subscribes to the Retrieved and Queried event handlers where any local objects which were fetched from the underlying data persistence layer are synthesized using their MASTER links \(and appropriate policies applied\).

## Behaviors

The following section outlines several common behaviors and patterns to assist in understanding how MDM works in SanteDB.

### Case 1: New Object Registered

When the CDR receives a request to create a new entity which is under MDM control, as shown below. 

![](../../../.gitbook/assets/image%20%28220%29.png)

1. The source record is issued a new UUID
2. The MDM layer will attempt to determine if the source record matches any MASTER records that currently exist within the database \(using the resource merge configuration\).
3. If no matching MDM MASTER is found, then the a new MASTER record is created and the SOURCE linked to the MASTER with its own UUID.
   1. The relationship is indicated with RelationshipType MDM-MASTER
   2. The classification of this relationship is AUTO

![](../../../.gitbook/assets/image%20%28215%29.png)

Any future queries based on the demographics will result in the MASTER\_A record being returned and synthesized from the source records according to the synthesization rules. 

![](../../../.gitbook/assets/image%20%28214%29.png)

### Case 2: Duplicate Object Created \(AutoLink Enabled\)

When the CDR receives a registration request for a new object which is under MDM control, such as shown below:

![](../../../.gitbook/assets/image%20%28213%29.png)

1. The source record is issued as new UUID
2. The IRecordMatchService is called with the specified configurations. If this process classifies a record as MATCH and AutoLink is turned on for that match configuration
   1. The SORUCE is linked to the MASTER with relationship MDM-Master 
   2. The classification of this relationship is AUTO
   3. The weighting of the match is stored

![](../../../.gitbook/assets/image%20%28223%29.png)

A query for EID A123 would now result in a single result with the synthesized data from both sources and links to the sources where the data was obtained.  


![](../../../.gitbook/assets/image%20%28216%29.png)

### Case 3: Suspected Duplicate Object Created \(or AutoLink disabled\)

When the CDR receives a request to create an object with similar attributes however as above, however:

* The attribute score from the fuzzy matching engine falls below the threshold of a definite match, or
* The automatic linking feature for the match configuration is disabled

Such as the patient illustrated below.

![](../../../.gitbook/assets/image%20%28218%29.png)

The behavior is as follows:

1. The SOURCE is issued a new UUID
2. A new MASTER is created with a new UUID
3. The SOURCE is linked to the new MASTER 
   1. The relationship type is MDM-Master
   2. The classification of the relationship is AUTO
4. The SOURCE is linked to the suspected MASTER 
   1. The relationship type is MDM-CandidateLocal
   2. The classification of the relationship is AUTO
   3. The score of the match is stored as the relationship strength

![](../../../.gitbook/assets/image%20%28219%29.png)

### Case 4: Object is Updated to Match MASTER

When the CDR receives a request to update a source record, it does so against the source \(or if the update was attempted against the MASTER the SOURCE is created or located\). When this occurs, the matching is re-run and if determined that the records now match the relationships are re-calculated. 

For example, given this update to SOURCE\_C.

![](../../../.gitbook/assets/image%20%28222%29.png)

The `SOURCE_C` record would be updated to match and the matching re-run, it may be determined that `SOURCE_C` is in fact the same person as `MASTER_A`

![](../../../.gitbook/assets/image%20%28217%29.png)

In this case, `SOURCE_C` is DETACHED from `MASTER_C` and then attached to `MASTER_A`.

### Case 5: Manual Reconciliation

The CDR also provides interfaces for manually reconciling candidate matches. Take for example, an instruction to reconcile `SOURCE_C` and `MASTER_A`.

![](../../../.gitbook/assets/image%20%28224%29.png)

In this method \(also known as a LOCAL&gt;MASTER merge\) the MDM-Candidate link is translated into a MDM-Master and the classification set to VERIFIED.

![](../../../.gitbook/assets/image%20%28212%29.png)

{% hint style="info" %}
Any operation which removes all MDM-Master links from a MASTER record will result in the automatic obsolete of the MASTER record.
{% endhint %}



