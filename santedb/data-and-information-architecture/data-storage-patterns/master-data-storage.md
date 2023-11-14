# Master Data Storage

The Master Data Management plugin permits your SanteDB CDR instance to store multiple copies of a single record based on the source system which provided the data. The MDM services are available on the following resources:

* Patient
* Place
* Provider
* Materials (and Manufactured Materials)
* Device Entities
* Persons

{% hint style="info" %}
The use of Master Data Management services require a compatible [Matching and Merge](broken-reference) service to operate. This is how the MDM solution detects candidate master records.
{% endhint %}

## MDM Data Storage Pattern

Within the data storage persistence layer, the MDM plugin will update/create locals using whatever underlying class was sent from the caller. Each caller is provided a complete copy of the record which they can update/edit.

The MDM plugin then determines:

* Is there a MASTER record which the IRecordMatching service has identified as positive match?
* Is the configuration enabled to automatically link these records?

If no MASTER is found, or the configuration does not permit auto-linking then a new MASTER of the base type is constructed (Entity in case of Patient, Place, Material, etc. or Act in the case of Administration, Procedure, Observation, etc.) and links the LOCAL record to this newly created master instance using the relationship type `MDM-MasterRecord`.



![](<../../../.gitbook/assets/image (268).png>)

The master record should have **no data** associated with it. It is merely an anchor which is used to collect the local records. Typically a master record can have extensions, notes, identifiers, names, etc. associated with it, however these attributes should apply to the anchor point rather than for establishing ROT data.

### Candidate Links

In the case where a match between a LOCAL and MASTER record is ambiguous (i.e. does is a Probable match or when Auto-Link is disabled) the link between records is considered a candidate and the local is related to the MASTERs which it is a candidate for using the `MDM-CandidateLocal` relationship type.

In the scenario below, Good Health Clinic has registered John Doe born Jan 1 1980 with ID 1230493. The MDM layer has constructed a master record. A subsequent registration by HIV Health Clinic for John Doe, born sometime in 1980 with ID 3029402 as registered after.

Assuming that the match configuration was setup such that the HIV record had a match score below "DEFINITE" match, the MDM plugin would establish a new MASTER which contains one LOCAL. That LOCAL would also be related to the MASTER from Good Health Clinic with relationship type `MDM-CandidateLocal`.\


![](<../../../.gitbook/assets/image (291).png>)

This candidate link exists until:

* A subsequent update from either the HIV Health Clinic (to record 3029402) or Good Health Clinic (to record 1230493) means that the patients no longer meet threshold for match.
* The match configuration is updated, which scores the link below the threshold for probable match.
* An administrator establishes a new link between the HIV Clinic and the MASTER of `MDM-IgnoreCandidate` (which indicates a known false-match).
* An administrator manually indicates that the HIV Health Clinic record is a known match to the MASTER (in which case the MDM-MasterRecord link is removed and updated (as shown below).

![](<../../../.gitbook/assets/image (632).png>)

### Record of Truth

The MDM solution permits the establishing of a Record Of Truth (ROT). The Record Of Truth is a new local instance which belongs to the SYSTEM and can only be updated when the security principal is permitted MDM Record Of Truth.&#x20;

A ROT record is a special pointer at a LOCAL whereby the LOCAL points to the MASTER record, and the MASTER points at the ROT with relationship type of `MDM-RecordOfTruth`.&#x20;

{% hint style="info" %}
It is possible to manually elevate an existing LOCAL as a ROT record, however this is not yet supported on user interfaces available.
{% endhint %}

![](<../../../.gitbook/assets/image (108).png>)



### Privacy Masking

It is a commonly asked how the solution operates when a sensitive LOCAL record is shared with common health infrastructure. In the case of SanteDB's iCDR, when a MASTER record has multiple LOCALS the information returned to a caller is a synthesized copy of data within the LOCAL records.

The synthetization process uses a most-restrictive policy enforcement mechanism before considering a local for inclusion in the result. In the example illustrated above, the information sourced from the HIV Health Clinic is tagged as TABOO information.&#x20;

When a caller asks the CDR for the MASTER, the MDM service will call the `IPolicyDecisionService` and ask for a decision on each of the flagged policies in each of the locals and will return either:

* The UNION of data from both Good Health Clinic and HIV Health Clinic when TABOO has a **GRANT**, or
* Only data from Good Health Clinic when TABOO policy outcome is **DENY**, or
* Only the data from Good Health Clinic and an indicator of elevation required (i.e. indicator more data is present) when the TABOO policy outcome is **ELEVATE.**



## MDM Service Relationships

The MdmDataManagementService should be configured in your application context. Upon start, this daemon will read the contents of the `ResourceMergeConfigurationSection` to determine the appropriate instances of `MdmResourceListener<T>` to construct and register with the provider.

![](<../../../.gitbook/assets/image (277).png>)

For example, given a configuration as provided below

```markup
<section xsi:type="ResourceMergeConfigurationSection">
  <resources>
    <add type="Patient" matchConfiguration="org.santedb.smpi.matching.default" autoMerge="false" />
    <add type="Place" matchConfiguration="org.santedb.shfr.matching.default" autoMerge="false" />
  </resources>
</section>
```

The MdmDataManagementService on start would register two resource listeners for Patient and Place. It would furthermore, instruct each resource listener to use the specified match configuration for detecting candidate local<>master linkages.

### MDM Resource Listener

The resource listener instances created by the data management service subscribe to the repository events for the indicated type. The resource listener receives an event broadcast from the repository service whenever an event occurs and takes appropriate actions.

#### Data Update Operations

The `Saving` and `Inserting` events of the repository service are subscribed on service start. Whenever data through a repository is being actioned the events are raised and the following actions occur on the MDM Resource Listener:

* The instances are validated through OnPrePersistenceValidate() method. Here the process ensures:
  * The caller is not attempting to update a MASTER record. If it is, the appropriate LOCAL for that principal is exchanged.
  * If the caller is attempting to create a RECORD OF TRUTH , it has appropriate permission to do so
* The Saving() and Inserting() event handlers are called next. These methods:
  * Call the matching service and attempt to establish whether the LOCAL is a candidate for an existing record
  * Appropriately obsolete/create resource links between the objects.
  * Cancels the caller (i.e. overwrites the default call path)
  * Returns a BUNDLE which is treated as a transaction on the persistence layer.

#### Data Query / Retrieval Operations

When a repository's `Find()` or `Get()` methods are called the repository will call the `Retrieving` and `Querying` event handlers. The MDM resource listener for that repository will perform the following operations:

* Cancel the default path of the repository
* Re-write the HDSI expression tree to query attributes related to the ROT or a LOCAL

The resource listener also subscribes to the Retrieved and Queried event handlers where any local objects which were fetched from the underlying data persistence layer are synthesized using their MASTER links (and appropriate policies applied).

## Behaviors

The following section outlines several common behaviors and patterns to assist in understanding how MDM works in SanteDB.

### Case 1: New Object Registered

When the CDR receives a request to create a new entity which is under MDM control, as shown below.&#x20;

![](<../../../.gitbook/assets/image (148).png>)

1. The source record is issued a new UUID
2. The MDM layer will attempt to determine if the source record matches any MASTER records that currently exist within the database (using the resource merge configuration).
3. If no matching MDM MASTER is found, then the a new MASTER record is created and the SOURCE linked to the MASTER with its own UUID.
   1. The relationship is indicated with RelationshipType MDM-MASTER
   2. The classification of this relationship is AUTO

![](<../../../.gitbook/assets/image (584).png>)

Any future queries based on the demographics will result in the MASTER\_A record being returned and synthesized from the source records according to the synthesization rules.&#x20;

![](<../../../.gitbook/assets/image (130).png>)

### Case 2: Duplicate Object Created (AutoLink Enabled)

When the CDR receives a registration request for a new object which is under MDM control, such as shown below:

![](<../../../.gitbook/assets/image (675).png>)

1. The source record is issued as new UUID
2. The IRecordMatchService is called with the specified configurations. If this process classifies a record as MATCH and AutoLink is turned on for that match configuration
   1. The SORUCE is linked to the MASTER with relationship MDM-Master&#x20;
   2. The classification of this relationship is AUTO
   3. The weighting of the match is stored

![](<../../../.gitbook/assets/image (785).png>)

A query for EID A123 would now result in a single result with the synthesized data from both sources and links to the sources where the data was obtained.\


![](<../../../.gitbook/assets/image (754).png>)

### Case 3: Suspected Duplicate Object Created (or AutoLink disabled)

When the CDR receives a request to create an object with similar attributes however as above, however:

* The attribute score from the fuzzy matching engine falls below the threshold of a definite match, or
* The automatic linking feature for the match configuration is disabled

Such as the patient illustrated below.

![](<../../../.gitbook/assets/image (744).png>)

The behavior is as follows:

1. The SOURCE is issued a new UUID
2. A new MASTER is created with a new UUID
3. The SOURCE is linked to the new MASTER&#x20;
   1. The relationship type is MDM-Master
   2. The classification of the relationship is AUTO
4. The SOURCE is linked to the suspected MASTER&#x20;
   1. The relationship type is MDM-CandidateLocal
   2. The classification of the relationship is AUTO
   3. The score of the match is stored as the relationship strength

![](<../../../.gitbook/assets/image (137).png>)

### Case 4: Object is Updated to Match MASTER

When the CDR receives a request to update a source record, it does so against the source (or if the update was attempted against the MASTER the SOURCE is created or located). When this occurs, the matching is re-run and if determined that the records now match the relationships are re-calculated.&#x20;

For example, given this update to SOURCE\_C.

![](<../../../.gitbook/assets/image (133).png>)

The `SOURCE_C` record would be updated to match and the matching re-run, it may be determined that `SOURCE_C` is in fact the same person as `MASTER_A`

![](<../../../.gitbook/assets/image (161).png>)

In this case, `SOURCE_C` is DETACHED from `MASTER_C` and then attached to `MASTER_A`.

### Case 5: Manual Reconciliation

The CDR also provides interfaces for manually reconciling candidate matches. Take for example, an instruction to reconcile `SOURCE_C` and `MASTER_A`.

![](<../../../.gitbook/assets/image (428).png>)

In this method (also known as a LOCAL>MASTER merge) the MDM-Candidate link is translated into a MDM-Master and the classification set to VERIFIED.

![](<../../../.gitbook/assets/image (585).png>)

{% hint style="info" %}
Any operation which removes all MDM-Master links from a MASTER record will result in the automatic obsolete of the MASTER record.
{% endhint %}

## Merging / Linking

Callers can directly manipulate the relationships using the `IRepositoryService<EntityRelationship>` services to implement custom logic for merging and linking. By default the MDM layer registers `IRecordMergeService<T>` instances which implement a default behavior for external calls to MERGE data.

| Victim Type | Survivor Type | No Permission | Write MDM           | Merge MDM           |
| ----------- | ------------- | ------------- | ------------------- | ------------------- |
| LOCAL       | LOCAL         | Local Merge   | Local Merge         | Local Merge         |
| LOCAL       | MASTER        | Local Merge   | Local/Master Relink | Local/Master Relink |
| MASTER      | MASTER        | Local Merge   | Local/Master Relink | Master Merge        |
|             |               |               |                     |                     |

### Local/Master Re-Link

A LOCAL>MASTER link operation is initiated by calling `Merge()` in `IRecordMergeService<T>` , and passing a UUID of a MASTER record and the linked duplicate UUIDs that are either:

* The explicit UUIDs of local records (i.e. the UUID pointing at the local record), or
* The UUID of masters where the caller does not have `Merge MDM Master` permission

This operation works by unlinking the local/duplicate record relationships (of `MDM-Master` ) and re-establishing the link on the locals to the surviving master. This is a form of linking where neither the master nor the local records are merged.&#x20;

For example, if a principal has `Write MDM Master` permission, and issues the following `ADT^A40` :

```markup
MSH|^~\&|TEST_HARNESS^^|TEST^^|CR1^^|MOH_CAAT^^|20141104174451|DEVICESECRET|ADT^A40^ADT_A39|TEST-CR-16-30|P|2.3.1
EVN||20101020
PID|||XXXXX^^^TEST||JONES^JENN^^^^^L||198401|F|||||||||||
MRG|YYYYY^^^TEST
```

The process would be:

* Load the record `XXXXX` in domain TEST (MASTER)
* Load the record `YYYYY` in domain TEST (MASTER)
* Call `Merge()` for MASTER>MASTER
* Client has `Write MDM Master` so record `XXXXX` remains the target of the merge.
* Client does not have `Merge MDM Master` so record `YYYYY` is resolved to LOCAL record for TEST\_HARNESS at site TEST (`LYYYY`)
* Merge proceeds as LOCAL>MASTER
  * `LYYYY` is disconnected from master `YYYY`
  * `LYYYY` is attached to master `XXXX`
  * If no further locals point at `YYYY` it is obsoleted.

### Master Merge

A MASTER to MASTER merge is the process whereby one master record is merged into another, and all associated LOCAL relationships are migrated to the survivor. Callers may only initiate a master merge when the principal carries the `Merge MDM Master` policy permission, otherwise an alternate merge strategy is used.

{% hint style="info" %}
Giving applications using the HL7v2 or HL7 FHIR interfaces permission for Merge MDM Master is not recommended as any use of a business identifier in those messages would result in a master merge, since the query stage loads master records on those interfaces.
{% endhint %}

The process for performing a master merge is:

* Load record `XXXX` in domain TEST (MASTER)
* Load record `YYYY` in domain TEST (MASTER)
* Call `Merge()` for MASTER>MASTER
* Client has `Write MDM Master` so record `XXXX` remains target of merge
* Client has `Merge MDM Master` so record `YYYY` remains source of merge
* Merge proceeds:
  * All `MDM-Master` associations previously pointing at `YYYY` are rewritten to `XXXX`
  * All identifiers directly on `YYYY` master record are copied to `XXXX`
  * `YYYY` is obsoleted&#x20;

### Local Merge

A local merge occurs when a source system indicates it has resolved duplicates in its own database issues an appropriate merge request to the iCDR. The local merge is the default operation whenever the caller is not granted explicit permission to perform MDM merges on the server.&#x20;

The process for performing a local merge is:

* Load record `XXXX` in domain TEST (MASTER)
* Load record `YYYY` in domain TEST (MASTER)
* Call `Merge()` for MASTER>MASTER
* Client does not have`Write MDM Master` so a local record for `XXXX` is resolved (`LXXXX`)
* Client does not have `Merge MDM Master` so a local record for `YYYY` is resolved (`LYYYY`)
* If `LYYYY` and `LXXXX` were resolved, then the merge occurs:
  * The record `LYYYY` is obsoleted
  * All identifiers from `LYYYY` are copied to `LXXXX` so that any query to `LYYYY` are resolved to the survivor
