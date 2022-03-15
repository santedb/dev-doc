# Master Data Management Tab

The **Master Data Management** tab is used to control the links controlled by the [master-data-storage.md](../../../../santedb/data-storage-patterns/master-data-storage.md "mention") plugin in SanteDB.&#x20;

{% hint style="info" %}
The Master Data Management tab will not appear when:

* The user does not have the appropriate MDM policy permissions
* The record being viewed is not under MDM control
* The MDM plugin is not enabled on the iCDR server
{% endhint %}

![](<../../../../.gitbook/assets/image (425).png>)

## Local Records

The local records panel shows the currently attached/established local or source records for the current master view (including the record of truth). These records are those which have been sent by a patient identity source (see: [#mdm-data-storage-pattern](../../../../santedb/data-storage-patterns/master-data-storage.md#mdm-data-storage-pattern "mention")). These are source records which are used to derive the master record (if no record of truth is established).

![](<../../../../.gitbook/assets/image (449).png>)

### Link Classification

The MDM layer captures the type of classification of link between the source record and its master. The types of classifications which are listed are:

| Classification | Description                                                                                                                                                                                                                         | Creation                                                                                                                                                           |
| -------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| System         | <p>The system classification indicates that the link was performed because the MDM plugin has established this link. <br>System links are never modified by the MDM layer unless needed to perform an unlink or link operation.</p> | <ul><li>New source record is registered with no definite master</li><li>Source is detached/unlinked from old master.</li></ul>                                     |
| Verified       | The link has been reviewed by a human and established for the source and master. The link is never modified by the MDM layer (they are sticky)                                                                                      | <ul><li>Administrator has resolved a candidate link.</li></ul>                                                                                                     |
| Auto           | The link has been established using an automatic merge rule in the match configuration or via unique identity domain.                                                                                                               | <ul><li>Patient with the same identifier in an identity domain listed as Unique</li><li>Match configuration with <code>$mdm.auto-link</code> set to true</li></ul> |

### Un-Linking

When a source record is unlinked from the master, the MDM layer will perform its unlinking logic.&#x20;

1. The relationship between the source and the current master is removed
2. A new master link for the unlinked source is created (with classification system)
3. An ignore instruction is added for the unlinked record and the old master (so they are not re-matched)
4. The re-match process is invoked

## Candidate Records

The candidates panel shows the identified [#candidate-links](../../../../santedb/data-storage-patterns/master-data-storage.md#candidate-links "mention") for the current master record.&#x20;

![](<../../../../.gitbook/assets/image (455).png>)

To resolve a candidate link:

1. View the details of the match to see the attributes in each record which were considered for matching.
2. If needed click on the **View** button to see details about the candidates.
3. Make a determination about the candidate pair:
   1. If the candidate is a match (they represent the same person) click the **Resolve** button to link the two&#x20;
   2. If the candidate is not a match (they represent different people) click the **Ignore** button&#x20;

### Match Details

Click on the candidate details button will open a popup window which illustrates the individual attribute values in both the current master and the candidate. This allows administrators to determine the reason why the two records are considered candidates for linking.

![](<../../../../.gitbook/assets/image (450) (1).png>)

## Ignored Candidates

The ignored candidates panel shows the list of candidate (source) records for the current master which are considered definite non-matches (and should be ignored for future matching).

![](<../../../../.gitbook/assets/image (435) (1).png>)

Like the candidates view, it is possible to perform gather an updated match report by clicking on **Details**. Users may also un-ignore the record if they feel the ignored (non-match) candidate may be a candidate for matching the master.

{% hint style="info" %}
If the source system (that which sent the data to the SanteMPI instance) updates their own information about the source record, then the data will be reflected in the ignored candidates row. It is possible that newer versions of the ignored patient may result in a previously ignored candidate becoming a match candidate (however due to the ignore statement they are excluded from the matching).
{% endhint %}
