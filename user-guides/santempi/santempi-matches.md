# SanteMPI Matches

SanteMPI provides a robust [matching-engine.md](../../santedb/matching-engine.md "mention")which can be used to determine whether new registrations or existing registrations are duplicate / identical patients.&#x20;

The matching dashboard is used to show the registered matches (i.e. those which have been detected and flagged) within the SanteMPI linkage tables.&#x20;

## Nomenclature

The nomenclature used in SanteDB is described in detail in [master-data-storage.md](../../santedb/data-storage-patterns/master-data-storage.md "mention"), when describing the patients in the user interface documentation the data will be referred to as:

* `LOCAL_A` - The source record submitted from a third party system, representing the `$input` record
* `MASTER_A` - The master/golden record established by SanteMPI's master data management layer for `LOCAL_A` (note there may be multiple locals attached to this record)
* `LOCAL_B` - The source record submitted from a third party system, representing the `$block` record
* `MASTER_B` - The master/golden record established by SanteMPI's master data management layer for `LOCAL_B` (note: there may be multiple locals attached to this record)

## Patient Matching

The first portion of the match dashboard shows the duplicate detection panel. This panel allows data administrators to quickly review duplicates which have been detected by the MPI software.

![](<../../.gitbook/assets/image (438) (1).png>)

* Candidate Report - Downloads the `Detected Duplicates` table in excel format
* Linkage Report - Downloads an excel report with the entirety of the SanteMPI database linkages provided.
* Candidate Patient A/B - The pair of patient records which were detected as a duplicate.
  * Patient A - The inbound or `$input or LOCAL_A` patient which was being registered
  * Patient B - The duplicate or `$block or MASTER_B` patient which was scored
* Normalized Score - The confidence (`0.0 .. 1.0`) that the patient represented in Patient A is the same as Patient B.
* [View Match Detail](santempi-matches.md#undefined) - Opens the detail screen for the match (see: )
* Quick Resolve - Resolves the match pair
* Quick Ignore - Ignores the match pair

### Quick Resolve

The quick resolution option allows the data administrator to quickly instruct the SanteMPI MDM layer that Patient A has been verified as Patient B. This action:

* Detaches `LOCAL_A` from `MASTER_A` (i.e. detaches the patient in Patient A column from its current master / golden record)
* Attaches `LOCAL_A` to `MASTER_B` (i.e. attaches the Patient A column to the Patient B master / golden record)
* If no further local or source records exist for `MASTER_A` then `MASTER_A` is obsoleted.

{% hint style="info" %}
The SanteMPI MDM user interfaces do not MERGE records, they change linkages. In SanteDB a MERGE is a different operation which is performed only by source systems when they send an appropriate `ADT^A40` or `PMIR Merge`
{% endhint %}

### Quick Ignore

The quick ignore option allows the data administrator to quickly instruct SanteMPI MDM layer that Patient A has been verified NOT to be Patient B. This action:

* Removes the current candidate record between `LOCAL_A` and `MASTER_B`
* Adds a new `Ignore` instruction which instructs all future detections between `LOCAL_A` and `MASTER_B` to be ignored.

## View Match Detail

Clicking on the `View` option, will display a more detailed analysis of the match pair. This view assists data administrators in determining the validity of the match, such that the match can be verified or ignored.

![](<../../.gitbook/assets/image (430) (1).png>)

* Match Summary Information Tab - Shows a side-by-side comparison of basic attributes on both the A and B records.
  * Either patient record can be opened using the `View` option.
* [A/B Comparison](santempi-matches.md#a-b-compare) - Shows the A and B comparison of all demographics for the patient match pair.
* [Scoring ](santempi-matches.md#undefined)- Shows a report of the match score between the two records based on configurations which are active in SanteMPI.
* Match Classification - Indicates the overall quality of the match

### A/B Compare

The `Matched Entities` tab shows summary information of the two patients which have been flagged as potential matches. However, there are times when a more holistic view of a patient match pair is desired. Some reasons the A/B compare may be used:

* To see other relationships both the A and B records have (such as citizenship, employment, marital status, multiple-birth, etc.)
* To view next of kin records on both A and B records.
* &#x20;To view additional identification information (from third party plugins) which would otherwise be rendered in the patient dashboard.

The A/B compare tab takes the contents of the [the-patient-dashboard.md](../../santempi/the-patient-dashboard.md "mention") (which is a common place for plugins to extend the UI) and shows the panels as an A/B comparison.

![](<../../.gitbook/assets/image (439) (1).png>)

### Scoring

The scoring tab presents a list of match configurations which are active on the SanteMPI server and presents each configured attribute, the weights, and calculated score.&#x20;

This panel is used by data administrators to understand **why** the particular match pair came to be flagged. This information is helpful when determining whether a configuration needs to be changed, or to understand why a match is a match.

![](<../../.gitbook/assets/image (418).png>)

* Classification - Indicates the match pair's classification as determined by the configuration.
* Match Method - The method or algorithm used to score the matches&#x20;
  * Weighted - The matching engine used a weighted scoring for the match
  * Deterministic - The matching engine used only a deterministic score for the match pair
  * Identifier - The matching engine made the determination based on identification of the source and target resources
* Absolute Score - The numeric score assigned to the match pair. This score is a sum of all weighted scores for all attributes.
* Strength - The normalized score which indicates on a scale of `0 .. 1` what the match agreement was.

The detail table illustrates the calculated (and weighted) score of each object (see: [matching-engine.md](../../santedb/matching-engine.md "mention")) for more details.

| E         | Indicates whether the attribute was even evaluated. If the attribute was not evaluated, then the `whenNull` action was taken on the score. | <p><span data-gb-custom-inline data-tag="emoji" data-code="2714">✔</span> - The attribute was evaluated and scored<br><span data-gb-custom-inline data-tag="emoji" data-code="2716">✖</span> - The attribute was not evaluated. The <code>whenNull</code> score was applied.</p> |
| --------- | ------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Attribute | Indicates the attribute identifier or name which was scored.                                                                               | The path to the property in A and B values.                                                                                                                                                                                                                                      |
| A Value   | The value of the property in record A which was evaluated.                                                                                 |                                                                                                                                                                                                                                                                                  |
| B Value   | The value of the property in record B which was evaluated.                                                                                 |                                                                                                                                                                                                                                                                                  |
| M / U     | Identifies the match probability (M) and the uncertainty (U) of the attributes.                                                            | <p>M - The likelihood that if the A value and B value agree, then the record represents a true match.<br>U - The likelihood that if the A value and B value agree, that they agree on a coincidence.</p>                                                                         |
| Score     | The numeric, calculated score given to the record (before partial scoring applied)                                                         |                                                                                                                                                                                                                                                                                  |
| Weight    | The final score applied to the overall score for the record.                                                                               |                                                                                                                                                                                                                                                                                  |

## Related Topics

{% content-ref url="the-patient-dashboard/master-data-management-tab.md" %}
[master-data-management-tab.md](the-patient-dashboard/master-data-management-tab.md)
{% endcontent-ref %}

{% content-ref url="matching-configuration/" %}
[matching-configuration](matching-configuration/)
{% endcontent-ref %}

{% content-ref url="../../santedb/matching-engine.md" %}
[matching-engine.md](../../santedb/matching-engine.md)
{% endcontent-ref %}
