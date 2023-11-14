# Testing Match Configuration

Testing a match configuration can be performed on the **Testing** tab. This tab allows administrators to either test:

* A single `$input` against the entirety of the SanteMPI iCDR database (testing blocking and scoring)
* A single `$input` against one or more manually provided `$block` records (testing for false negatives)

## Establishing a $input Context

First, users should search for a `$input` record for which they would like to test their configuration. The search is performed by identifier, as an example, a patient has been selected and selected.

![](<../../../.gitbook/assets/image (445) (1) (1).png>)

If performing a match test against the underlying data store, the user can press the **Run** button.

### Manual $block Records



## Test Results

Once test results are available they are gathered and the data displayed in a series of panels.

### Test Overview Panel

The overview panel shows summary information about the test results. These summary indicators provide a brief insight into scores from results of the test run.

![](<../../../.gitbook/assets/image (459) (1).png>)

### Hints / Analysis

The hints and analysis panel provides (currently, basic) feedback on your configuration and how it could be optimized. The panel checks for:

* Excessive records being loaded from the database (i.e. > 10% of the blocked records were discarded or non-matches. Which indicates too many results are being loaded form database)
* Too restrictive scoring or inappropriate blocking (i.e. many records are blocked but none are matched)

![](<../../../.gitbook/assets/image (446) (1) (1).png>)

### Match Test Results

The test results panel show the individual records which were evaluated (up to 100 of them) against the input record. This includes basic demographics information about the match pair, the score assigned from evaluation and the classification.

![](<../../../.gitbook/assets/image (456) (1) (1).png>)

Users may select the **view** option to see a detailed report of the attributes which were considered and the values which were compared as well as the computed score of the current configuration compared with other configurations).

For example, one of the non-match records, by viewing the data, can be seen that the state of the records match however the city do not. Resulting in the computed score.

![](<../../../.gitbook/assets/image (429) (1).png>)

{% hint style="info" %}
The settings for the match configuration can be changed on the [blocking-configuration.md](blocking-configuration.md "mention") , [scoring-configuration.md](scoring-configuration.md "mention") or [classification-configuration.md](classification-configuration.md "mention") tabs and re-tested in an iterative fashion to tune your match configuration.
{% endhint %}

Additionally, the administrator can review the full details of how this match pair would appear in the [santempi-matches.md](../santempi-matches.md "mention") screen by clicking on **Details** (although merge and ignore functions are disabled).

### Test Result

The test result diagram shows the flow of actual data through the match configuration test run. This data is fed by telemetry information in the matching engine as the test is executed.

![](<../../../.gitbook/assets/image (424).png>)

The diagram above illustrates:

* Blocking:
  * 532,061 records of type Patient were found in the database (the total population of patients which could be considered for matching)
  * 2 records were blocked because they had a matching SSN number (or the SSN number matched as configured in the blocking section)
  * 2 records were blocked based on the demographic data of Family, Gender and State
* Scoring
  * 3 total records were treated as `$block` records into the address, name, and address attribute scores (1 record was most likely excluded from blocking since the `$input` itself matches the data)
  * 3 of the `$block` records matched the first attribute score instruction (the state and country match)
  * 0 of the records passed the evaluation of name attribute
  * 1 records passed the evaluation of the city attribute score
* Classification
  * 2 records scored below the minimum threshold for a probable match and were classified as non-matches.
  * 0 records scored above the minimum threshold for a probable match and below the minimum  threshold for a definite match
  * 1 records scored above the minimum threshold of a match and was classified as such.
