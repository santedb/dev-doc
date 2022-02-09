# Scoring Configuration

## Attribute Scores

As described in the [matching-engine.md](../../../santedb/matching-engine.md "mention") architecture article, scoring is the process whereby a blocked record has its properties/attributes compared and scored between the `$input` and `$block` records. Attribute scores, like blocks in the blocking configuration are displayed in an accordion control.

![](<../../../.gitbook/assets/image (450).png>)

Each scored attribute contains:

* An explain diagram of the particular blocking instruction. The instructions are shown as a flow diagram (from left to right) and illustrate the logic of the attribute scoring process.
* The attribute identifier (optional) which is used in logs and by other attributes to refer to the attribute decision logic.
* The property(ies) which are extracted and used as the initial source data for the attribute.
* The null handling condition which dictates how missing data should be handled.
* The transforms (if any) which are applied to the input values prior to assertion evaluation.
* The evaluation / assertion which is made.
* The scoring information such as the M and U values and the match and non-match weights.
* Any partial scoring methodology applied to score.

## Editing Attributes

Users can edit the scored attribute list to modify scored attributes and/or add new attributes to the configuration.

![](<../../../.gitbook/assets/image (446).png>)

New attributes for scoring can be added with the `Add Scored Attribute` button and removed with the `Remove Scored Attribute` button on each attribute. A match configuration must contain at least one scoring statement.

{% hint style="info" %}
When editing a scored attribute, the explain diagram for that attribute is automatically updated to provide a graphical representation of the attribute data.
{% endhint %}

### Attribute Information

The first section of the attribute configuration are descriptive fields (ID and Notes) and the selector (the HDSI expression that extracts the values from `$input` and `$block`). For example, to score based on the patient's home address state, the administrator may provide an attribute id, a note, and an extraction path of `address[HomeAddress]`.&#x20;

![](<../../../.gitbook/assets/image (427).png>)

{% hint style="info" %}
Note that the property extraction is to the root element rather than the value element of `address[HomeAddress].component[State].value` , this is done since the extraction of the root property allows for more granular transforms (i.e. we can perform multiple extractions on the address property rather than just the state portion).
{% endhint %}

#### Multiple Properties

If the administrator wishes to provide multiple paths for extraction they can provide either a single HDSI expression or multiple properties in the property list. For example, if `HomeAddress` or `VacationHome` they may provide separate extraction properties.

![](<../../../.gitbook/assets/image (451).png>)

This instructs the scoring engine to attempt an extract of `HomeAddress` from both `$input` and `$block`. If either are null, then an attempt is made to extract `VacationHome` from both `$input` and `$block`.&#x20;

{% hint style="warning" %}
The HDSI expression `address[HomeAddress|VacationHome]` is also a valid extraction expression, however the semantic meaning differs. If using an OR statement in your HDSI expression guard this indicates that either type of address from `$block` or `$input` may be considered. For example, `$block.address[VacationHome]` may be compared to `$input.address[HomeAddress]`. Separating the property extraction expressions ensures that the same types of addresses are compared.
{% endhint %}

### When Null Behavior

The **When Null** input on the attribute instructs the scoring process, how to handle the case when data is missing from either `$block` or `$input`.&#x20;

| When Null  | Behavior                                                                                                                                                                                                                                                                                        | Diagram                                         |
| ---------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------- |
| None       | No special behavior is performed. The assertions are evaluated as specified.                                                                                                                                                                                                                    | ![](<../../../.gitbook/assets/image (421).png>) |
| Zero       | When the value extracted form  `$input` or `$block` are null, a score of 0 is assigned to the attribute.                                                                                                                                                                                        | ![](<../../../.gitbook/assets/image (443).png>) |
| Disqualify | When the value extracted from `$input` or `$block` are null, the entirety of `$input` and `$block` are assigned a non-match score (a score of negative infinity)                                                                                                                                | ![](<../../../.gitbook/assets/image (439).png>) |
| Match      | When a value extracted from `$input` and `$block` are null, then the attribute is assumed to have matched and the matchWeight is applied.                                                                                                                                                       | ![](<../../../.gitbook/assets/image (448).png>) |
| NonMatch   | When a value extracted from `$input` or `$block` are null, then the attribute is assumed to have not-matched and the nonMatchWeight is applied.                                                                                                                                                 | ![](<../../../.gitbook/assets/image (441).png>) |
| Ignore     | When a value extracted  from `$input` or `$block` are null, then the attribute is ignored. The attribute is assigned a score of 0 and the total weight which the records under consideration could have is decreased (i.e. it is as though, for that pair, the attribute was never configured). | ![](<../../../.gitbook/assets/image (449).png>) |

### Attribute Transforms



### Evaluation / Assertions



### M and U Values



### Partial Weights

### Attribute Dependencies / Evaluation Guards



## Explain Diagram

