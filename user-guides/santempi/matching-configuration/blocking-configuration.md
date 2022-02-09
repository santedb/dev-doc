# Blocking Configuration

## Blocking Filters

The blocking filters panel on the blocking configuration tab allows administrators to view and edit the filters which will be used to block data from the underlying data persistence source to select candidates which may be a good candidate for the more computationally complex process of scoring.

![](<../../../.gitbook/assets/image (441).png>)

Each block (or group of filters) is shown in an accordion which can be expanded using the **Block 0** through **Block n** links. Each block contains:

* Batch Size: Which dictates how many records at a time should be loaded from the underlying persistence layer.
* Block Strategy: Identifies the manner in which candidates are loaded from the database for scoring.
  * MASTER - Database records loaded / considered from the persistence layer are synthesized according to the MDM rules before being scored (slower but may be more accurate depending on the quality of input data)
  * SOURCE - Database records are loaded / considered from the persistence layer are not synthesized according to MDM rules. Only the information submitted from source systems is considered (faster, but may be less accurate depending on quality of input data).
* Notes Human readable notes about the blocking filter.
* Set Operation: Indicates the manner in which the block is included with other blocks in this configuration.
  * INTERSECT - Records from previous blocks are intersected with those in the current block. This means that a record must appear in both block statements to be considered for scoring (logically an AND function between filters).
  * UNION - Records from the previous blocks are appended in a union function. This means that distinct records from both blocks are included and considered for scoring (logically an OR function between filters).
* Block Filters: The [hdsi-query-syntax](../../../developers/service-apis/health-data-service-interface-hdsi/hdsi-query-syntax/ "mention") expressions that will be translated into SQL to load data from the underlying database.

### Editing Blocks

Users can edit blocking instructions by clicking the pencil on the blocking instruction panel.

![](<../../../.gitbook/assets/image (454).png>)

When in edit mode, the administrator should configure the settings for each block with the provided inputs.

The blocking filters should follow the [hdsi-query-syntax](../../../developers/service-apis/health-data-service-interface-hdsi/hdsi-query-syntax/ "mention") and adhere to the [#and-or-semantics](../../../developers/service-apis/health-data-service-interface-hdsi/hdsi-query-syntax/#and-or-semantics "mention") of the HDSI query grammar. The blocking configuration combines each statement as a singe query expression which is sent to the persistence layer.

{% hint style="info" %}
Implementers should take into consideration the performance characteristics of any [filter-functions.md](../../../developers/service-apis/health-data-service-interface-hdsi/hdsi-query-syntax/filter-functions.md "mention") which are used in their blocking configuration. It is recommended that indexed functions (like `similarity`, `similarity_lev`, `soundex`, etc.) be used over operations which require table scans (like `levenshtein`, `substring`, etc.).&#x20;

The same rules which apply to filter functions on the [santempi-power-search.md](../santempi-power-search.md "mention") page apply to the blocking configuration (i.e. the database technology used must support the filter function)&#x20;
{% endhint %}

### Multiple Blocks

Blocks are loaded as atomic queries, however there are situations where implementers may wish to load multiple types of patients from the database for consideration. This is done using multiple blocking instructions.&#x20;

For example, the following blocking instruction would load patients where a record in the database has a gender, name, state, and SSN which match the `$input` criteria.

![](<../../../.gitbook/assets/image (429).png>)

However, a jurisdiction may wish to block patients whose gender, name, state match OR has a matching SSN. In this case two blocks would be defined. To do this the jurisdiction would remove the SSN clause from the first block, and would, instead, create a second block for just SSN and UNION the two blocks together:

![](<../../../.gitbook/assets/image (425).png>)

## Explain Diagram

The explain diagram presented in the blocking tab shows a detailed blocking data flow from the source database resource type to the scoring stage.

![](<../../../.gitbook/assets/image (426).png>)

The explain diagram focuses on the blocking stage and can show additional information about gathering of records, the set operations, etc.&#x20;

## Related Topics

{% content-ref url="scoring-configuration.md" %}
[scoring-configuration.md](scoring-configuration.md)
{% endcontent-ref %}

{% content-ref url="../../../developers/service-apis/health-data-service-interface-hdsi/hdsi-query-syntax/" %}
[hdsi-query-syntax](../../../developers/service-apis/health-data-service-interface-hdsi/hdsi-query-syntax/)
{% endcontent-ref %}

{% content-ref url="../../../developers/service-apis/health-data-service-interface-hdsi/hdsi-query-syntax/filter-functions.md" %}
[filter-functions.md](../../../developers/service-apis/health-data-service-interface-hdsi/hdsi-query-syntax/filter-functions.md)
{% endcontent-ref %}

{% content-ref url="../santempi-power-search.md" %}
[santempi-power-search.md](../santempi-power-search.md)
{% endcontent-ref %}
