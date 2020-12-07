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

