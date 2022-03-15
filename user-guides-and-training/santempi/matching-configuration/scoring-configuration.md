# Scoring Configuration

## Attribute Scores

As described in the [matching-engine.md](../../../santedb/matching-engine.md "mention") architecture article, scoring is the process whereby a blocked record has its properties/attributes compared and scored between the `$input` and `$block` records. Attribute scores, like blocks in the blocking configuration are displayed in an accordion control.

![](<../../../.gitbook/assets/image (453) (1).png>)

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

![](<../../../.gitbook/assets/image (448) (1).png>)

New attributes for scoring can be added with the `Add Scored Attribute` button and removed with the `Remove Scored Attribute` button on each attribute. A match configuration must contain at least one scoring statement.

{% hint style="info" %}
When editing a scored attribute, the explain diagram for that attribute is automatically updated to provide a graphical representation of the attribute data.
{% endhint %}

### Attribute Information

The first section of the attribute configuration are descriptive fields (ID and Notes) and the selector (the HDSI expression that extracts the values from `$input` and `$block`). For example, to score based on the patient's home address state, the administrator may provide an attribute id, a note, and an extraction path of `address[HomeAddress]`.&#x20;

![](<../../../.gitbook/assets/image (427) (1).png>)

{% hint style="info" %}
Note that the property extraction is to the root element rather than the value element of `address[HomeAddress].component[State].value` , this is done since the extraction of the root property allows for more granular transforms (i.e. we can perform multiple extractions on the address property rather than just the state portion).
{% endhint %}

#### Multiple Properties

If the administrator wishes to provide multiple paths for extraction they can provide either a single HDSI expression or multiple properties in the property list. For example, if `HomeAddress` or `VacationHome` they may provide separate extraction properties.

![](<../../../.gitbook/assets/image (455) (1) (1).png>)

This instructs the scoring engine to attempt an extract of `HomeAddress` from both `$input` and `$block`. If either are null, then an attempt is made to extract `VacationHome` from both `$input` and `$block`.&#x20;

{% hint style="warning" %}
The HDSI expression `address[HomeAddress|VacationHome]` is also a valid extraction expression, however the semantic meaning differs. If using an OR statement in your HDSI expression guard this indicates that either type of address from `$block` or `$input` may be considered. For example, `$block.address[VacationHome]` may be compared to `$input.address[HomeAddress]`. Separating the property extraction expressions ensures that the same types of addresses are compared.
{% endhint %}

### When Null Behavior

The **When Null** input on the attribute instructs the scoring process, how to handle the case when data is missing from either `$block` or `$input`.&#x20;

| When Null  | Behavior                                                                                                                                                                                                                                                                                        | Diagram                                                 |
| ---------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------- |
| None       | No special behavior is performed. The assertions are evaluated as specified.                                                                                                                                                                                                                    | ![](<../../../.gitbook/assets/image (422).png>)         |
| Zero       | When the value extracted form  `$input` or `$block` are null, a score of 0 is assigned to the attribute.                                                                                                                                                                                        | ![](<../../../.gitbook/assets/image (447) (1).png>)     |
| Disqualify | When the value extracted from `$input` or `$block` are null, the entirety of `$input` and `$block` are assigned a non-match score (a score of negative infinity)                                                                                                                                | ![](<../../../.gitbook/assets/image (440) (1) (1).png>) |
| Match      | When a value extracted from `$input` and `$block` are null, then the attribute is assumed to have matched and the matchWeight is applied.                                                                                                                                                       | ![](<../../../.gitbook/assets/image (451) (1).png>)     |
| NonMatch   | When a value extracted from `$input` or `$block` are null, then the attribute is assumed to have not-matched and the nonMatchWeight is applied.                                                                                                                                                 | ![](<../../../.gitbook/assets/image (442) (1).png>)     |
| Ignore     | When a value extracted  from `$input` or `$block` are null, then the attribute is ignored. The attribute is assigned a score of 0 and the total weight which the records under consideration could have is decreased (i.e. it is as though, for that pair, the attribute was never configured). | ![](<../../../.gitbook/assets/image (452) (1) (1).png>) |

### Attribute Transforms

The matching attribute evaluation can be considered a type of data flow. Consider our example using address, the flow of data in the evaluation of the transform may initially resemble

![](<../../../.gitbook/assets/image (449) (1) (1).png>)

The steps which would be executed are:

* Extract `address[HomeAddress]` from both `$input` and `$block` and store them in variables `$a` and `$b` respectively.
* Determine if `$a` == `$b` (using the `.Equals`) method.
* If true, assign a score of +5.5
* If false, assign a score of -3.1

However, the attribute in our example is intended to be the state, the intent is not to compare the entirety of the home address.&#x20;

This is where transforms are used. A transform is applied to both the `$a` and `$b` values extracted from `$input` and `$block`.

Transforms can be added by clicking the `Add Value Transform` to the configuration. Transforms are applied to both the `$a` and `$b` values and can be either a binary or unary transform (see: [#implementing-custom-idatatransform-for-scoring](../../../developers/server-plugins/custom-algorithms.md#implementing-custom-idatatransform-for-scoring "mention"))&#x20;

* Binary Transforms - Are transforms which take `$a` and `$b` as their input and produce a single output result.
* Unary Transforms - Are transforms which accept either `$a` or `$b` as their input and produce a single result which is re-assigned to `$a` and `$b`.&#x20;

For example, adding the **Address Part Extract** to the attribute configuration and specifying `City` as the parameter:

![](<../../../.gitbook/assets/image (438) (1) (1).png>)

Can be translated to : Extract the `State` part from both `$a` and `$b` addresses. This is reflected in the explain diagram as a transform.

![](<../../../.gitbook/assets/image (432) (1) (1) (1).png>)

If the `$input` address contained `123 Main Street West, Some City, Some State, Some Country` and the `$block` address contained `321 West 5th St., Some Other City, Some State, Some Country` then the data flow would be:

| Step                         | $a                                                        | $b                                                             |
| ---------------------------- | --------------------------------------------------------- | -------------------------------------------------------------- |
| Extract `HomeAddress`        | 123 Main Street West, Some City, Some State, Some Country | 321 West 5th Street, Some Other City, Some State, Some Country |
| addresspart\_extract (State) | Some State                                                | Some State                                                     |
| Assert ? ==                  | true                                                      |                                                                |

If the state is selected from a drop down or a known codification of states, then this may be sufficient. However, if the state entry is a free-text input, the implementer may wish to apply a string comparison operation (a binary transform) of levenshtein string difference to both inputs.

![](<../../../.gitbook/assets/image (433) (1).png>)

The related data flow here, would be expressed as:

![](<../../../.gitbook/assets/image (428) (1).png>)

Tracing data from the example above, the evaluation of the attribute is now performed as:

| Step                         | $a                                                        | $b                                                             |
| ---------------------------- | --------------------------------------------------------- | -------------------------------------------------------------- |
| Extract `HomeAddress`        | 123 Main Street West, Some City, Some State, Some Country | 321 West 5th Street, Some Other City, Some State, Some Country |
| addresspart\_extract (State) | Some State                                                | Some State                                                     |
| levenshtein                  | 0                                                         |                                                                |
| Assert ? < 2                 | true                                                      |                                                                |

#### Unary Transforms

| Transform            | Parameters                                                                                                                                                                                                                                                                                                                         | Returns                                                                                                                                                                                                                                                                |
| -------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Timespan Extract     | <ul><li><p><code>part</code></p><ul><li>y - Years</li><li>M - Months</li><li>q - Quarter</li><li>d - Days</li><li>w - Weeks</li><li>h - hours</li><li>m - Minutes</li><li>s - Seconds</li></ul></li></ul>                                                                                                                          | The specified part of the timespan from each input variable.                                                                                                                                                                                                           |
| Double Metaphone     |                                                                                                                                                                                                                                                                                                                                    | The double metaphone phonetic code for the inputs.                                                                                                                                                                                                                     |
| Length               |                                                                                                                                                                                                                                                                                                                                    | The string length (in characters) of the inputs                                                                                                                                                                                                                        |
| Metaphone            |                                                                                                                                                                                                                                                                                                                                    | The metaphone phonetic code of each input.                                                                                                                                                                                                                             |
| Soundex              |                                                                                                                                                                                                                                                                                                                                    | The soundex phonetic code of each input (useful for English given names)                                                                                                                                                                                               |
| Substring            | <ul><li><code>start</code> The start position in the string</li><li><code>length</code> The amount of characters to extract.</li></ul>                                                                                                                                                                                             | The extracted portion of the string.                                                                                                                                                                                                                                   |
| Tokenize             | <ul><li><code>delimiter</code> The character(s) in the string which should be tokenized on.</li></ul>                                                                                                                                                                                                                              | A tokenized string. This function will split each of the inputs on the specified split characters. This is useful in languages like Burmese where names are broken into parts (example: `Ni Ni Win` and `Nih Nih Wihn`)  can be tokenized and then phonetically coded. |
| Absolute Value       |                                                                                                                                                                                                                                                                                                                                    | When used on a number, provides the absolute value of the inputs.                                                                                                                                                                                                      |
| Date Extract         | <ul><li><p><code>part</code> The part of the date to extract</p><ul><li>y - Years</li><li>M - Month of year</li><li>d - Day of month</li><li>D - Day of week</li><li>q - Quarter</li><li>w - Week of year</li><li>S - Semester</li><li>h - Hour of day</li><li>m - Minute of hour</li><li>s - Second of minute</li></ul></li></ul> | The extract date part                                                                                                                                                                                                                                                  |
| Address Part Extract | <ul><li><p><code>part</code> - The part of the address to extract</p><ul><li>Country</li><li>State</li><li>County</li><li>City</li><li>Precinct</li><li>Street</li></ul></li></ul>                                                                                                                                                 | The extracted part of the input address of each value.                                                                                                                                                                                                                 |
| Name Part Extract    | <ul><li><p><code>part</code> The part of the name to be extracted.</p><ul><li>Prefix</li><li>Given</li><li>Family</li><li>Suffix</li></ul></li></ul>                                                                                                                                                                               | The extracted part of the input name of each value.                                                                                                                                                                                                                    |

#### Binary Transforms

| Transform                     | Returns                                                                                                                                                        |
| ----------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Jaro-Winkler                  | The jaro-winkler string difference (from 0..1.0, with higher numbers being more similar strings) between inputs                                                |
| Levenshtein String Difference | The number of edits (whole number of edits) which would need to be applied to `$a` to transform it into `$b`.                                                  |
| Similarity To                 | Computes the % similarity between `$a` and `$b` by taking the levenshtein string difference of the two and dividing it by the longer of `$a` or `$b`           |
| Sorensen Dice                 | Calculates the sorensen dice coefficient of the two inputs.                                                                                                    |
| Date Difference               | Calculates the span of time between `$a` and `$b` (to extract a part of the result, use the timespan extract)                                                  |
| Name Alias Lookup             | Calculates the strength between the two names if they are aliases of one another. For example, Will is a strong alias for William and a weaker alias for Bill. |

### Evaluation / Assertion

The final step of the evaluation section is the assertion. The assertion is used to determine the logical operation which occurs between the output of all transforms for `$a` and `$b`. The transforms available will depend on the type of transform and the resulting value.

When a simple assertion is provided, or only unary transforms are used the options for the transform are:

* A Equal B - True when both the `$a` and `$b` values are value equal one another
* A NotEqual B - True when the `$a` and `$b` values are values do not equal to another.

If a binary transform has been performed, then users may select a comparison value and an operator.

* &#x20;result Equal - True when the binary transform result equals the provided value
* result NotEqual - True when the binary transform result is not equal to the provided value
* result LessThan - True when the binary transform result is less than the provided value
* result LessThanOrEqualTo - True when the binary transform result is less than or equal to the provided value
* result GreaterThan - True when the binary transform result is greater than the provided value
* result GreatThanOrEqualTo - True when the binary result is greater than or equal to the provided value.

#### Multiple Assertions

There are scenarios when an administrator may wish to execute multiple assertions on different pieces of data. In this case, the administrator will click the **Add Sub-Assertion** which is present when no transforms are applied to the values. The administrator can then select an operator:

* A AndAlso B - True when all the sub-assertions evaluate to TRUE
* A OrElse B - True when any of the sub-assertions evaluate to TRUE.

The administrator then configures each sub-assertion as they would a normal assertion.&#x20;

Continuing the example above, perhaps the administrator would like the logic to score the state only if the country code also matches.&#x20;

![](<../../../.gitbook/assets/image (458).png>)

The explanation flow diagram will be updated to reflect that multiple assertions are being made independently and then the logical operator selected applied.

![](<../../../.gitbook/assets/image (431) (1).png>)

### M and U Values

The scoring engine requires information in order to assign a match and non-match weight. These are set by using the **m** and **u** values. These values are defined as:

* `m` - The likelihood that, if the two values agree, the represent a true positive match (you can think of this as the match probability)
* `u` - The likelihood that, if the two values agree, they agree by pure coincidence (you can think of this as the uncertainty or coincidence).

the M and U values can be set in the user interface by either sliding the indicators to adjust the values, or by entering an exact number.

![](<../../../.gitbook/assets/image (444) (1) (1).png>)

The calculated scores are shown below the entry for M and U. These scores are calculated via $$weight_m=\frac{log_e(\frac{m}{u})}{log_e(2.0)}$$ and $$weight_u=\frac{log_e(\frac{1-m}{1-u})}{log_e(2.0)}$$.

#### Tips for Estimating M and U

Estimating the **u** value can be performed by taking a simple probability that two values will agree by coincidence. This can be done by taking a sample of distinct possible values and inverting them. For example:

* Week of Birth  $$u=\frac{1}{52} =0.19$$&#x20;
* Canadian provinces and territories $$u=\frac{1}{13} = 0.07$$
* Month of year $$u=\frac{1}{12}=0.083$$

Estimating the **m** value is a little more tricky, it indicates the likelihood that values matching represent a true positive match. The best recommendation for estimating the **m** is to set a reasonable initial value and then monitor the performance of the match configuration or use the machine learning optimizer provided by SanteSuite partner Hamilton Health Sciences ([https://github.com/santedb/configuration\_optimizer](https://github.com/santedb/configuration\_optimizer)).&#x20;

{% hint style="info" %}
If using the configuration optimizer it is important that administrators establish some sort of ground truth. The process for this is:

1. Create an initial set of match configuration parameters
2. Run the `Background Matching Job` to establish a baseline of matches
3. Use the [santempi-matches.md](../santempi-matches.md "mention") screen to flag true-positives (i.e. matches) and false-positives (i.e. non-matches)
4. Run the configuration optimizer against the SanteDB instance via its middleware for 3-4 optimizations
5. Review the modified configuration weights and - if satisfied - activate these changes&#x20;
6. Repeat steps 2 - 5.
{% endhint %}

### Partial Weights

Partial weights are used to control cases where the assertion of the attribute evaluates to TRUE however the values themselves differ.

Consider, for example, an evaluation of given name where the transforms are:

1. Extract the given name part of the value
2. Apply a metaphone phonetic code

The flow of this evaluation would be illustrated as:

![](<../../../.gitbook/assets/image (421) (1).png>)

In this configuration, if `$input` has a given name of `Kimberly` then the following `$block` records would match and all would be assigned a score of 3.2.

| Name              | namepart\_extract | dmetaphone | assertion |
| ----------------- | ----------------- | ---------- | --------- |
| Kimberleigh Smith | Kimberleigh       | KMPR       | PASS      |
| Kimberly Smith    | Kimberly          | KMPR       | PASS      |
| Kimber Smith      | Kimber            | KMPR       | PASS      |

However, looking at the source data, we can see that each of the blocks are not equally strong. SanteDB provides a mechanism for modifying the resulting score based on some algorithm. For example, we could apply a similarity to partial weight.

![](<../../../.gitbook/assets/image (423) (1).png>)

Similarity returns a value between `0.0 .. 1.0` , based on the string similarity with higher numbers being more similar strings. This means that our score of `3.2` would now be adjusted based on the similarity of the input strings. With this modification:

| Name              | similarity | Score  |
| ----------------- | ---------- | ------ |
| Kimberleigh Smith | 0.429      | 1.3728 |
| Kimberly Smith    | 1.0        | 3.2    |
| Kimber Smith      | 0.715      | 2.288  |

### Attribute Dependencies / Evaluation Guards

Some cases arise where implementers may wish to evaluate two properties independently of each other, but one is dependent on another. A common use of this is `City` where we may wish to evaluate the `City` based on a levenshtein string difference, however only if the `State` matched (since a Kansas City MO is different than Kansas City KY).

To do this, the Evaluation Guard property is used. In order to relate two attributes:

* The dependent attribute must appear in the configuration (and be evaluated) prior to the current.
* The dependent attribute must have an ID

Using the example above, if the city portion of the home address were to be evaluated, then a dependency to the `address_state` attribute created above must be linked:

![](<../../../.gitbook/assets/image (435) (1) (1) (1).png>)

## Explain Diagram

The explain diagram on the scoring tab shows the detailed blocking logic of the configuration. Users are able to see the concrete steps which, in the general tab, are only displayed as procedures.

![](<../../../.gitbook/assets/image (439) (1) (1).png>)

## Related Topics

{% content-ref url="../../../developers/service-apis/health-data-service-interface-hdsi/hdsi-query-syntax/" %}
[hdsi-query-syntax](../../../developers/service-apis/health-data-service-interface-hdsi/hdsi-query-syntax/)
{% endcontent-ref %}

{% content-ref url="../../../santedb/matching-engine.md" %}
[matching-engine.md](../../../santedb/matching-engine.md)
{% endcontent-ref %}

{% content-ref url="blocking-configuration.md" %}
[blocking-configuration.md](blocking-configuration.md)
{% endcontent-ref %}
