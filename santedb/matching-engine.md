# Matching Engine

{% hint style="info" %}
SanteMPI uses the SanteDB matching engine. This page may be moved in the future to a common page as the SanteDB matching engine supports more than just Patient resources.
{% endhint %}

The matching engine in SanteDB is a multi-stage process whereby an inbound (or a target record) is compared with the current dataset within the CDR. The matching process occurs in three stages:

* **Blocking :** In the blocking phase records are queried from the CDR's database infrastructure. The blocking phase is used to reduce the total number of records being scored, which can be more computationally expensive.
* **Scoring :** In the scoring stage, the target record is compared to those records retrieved from the blocking phase. Each attribute configured is transformed/normalized and then a score applied for each attribute. Furthermore there are API hooks for implementing partial weighting/partial scoring of an attribute (based on frequency of data in database, NLP, or other future methods)
* **Classification :**  In the classification stage, each record's score (the sum of each attribute's score) is grouped into Match, NonMatch, and ProbableMatch. These thresholds are configured.

SanteDB allows for the configuration of multiple match configurations, and allows configuration for the "default" match configuration to be used for regular operation (whenever data is inserted, updated, etc.).

## Match Configuration

Matches are configured using match configuration XML, the schema for this XML can be located in %INSTALL\_DIR%\Schemas and referenced in an XML editor of your choice to obtain auto-complete data.

### Target and Classification Thresholds

All match configurations begin with the **\<MatchConfiguration>** element. This element defines the overall matching process you'd like to apply.

```markup
<MatchConfiguration xmlns="http://santedb.org/matcher"
                    id="test.complex"
                    nonmatchThreshold="1"
                    matchThreshold="3.4">                    
```

The attributes for this element are:

| Attribute         | Type       | Description                                                                                              |
| ----------------- | ---------- | -------------------------------------------------------------------------------------------------------- |
| id                | xs:string  | A unique identifier for this match configuration, used when configuring any triggers which use matching. |
| nonmatchThreshold | xs:decimal | The threshold at which a candidate is excluded from consideration as being a match.                      |
| matchThreshold    | xs:decimal | The threshold at which a candidate is considered a definite match.                                       |

The next element to be configured is the target resource and triggers. Note that some SanteDB Components don't adhere to these settings, they are for suggestion only.

```markup
  ...
  <target resource="Patient">
    <event>BeforeInsert</event>
    <event>BeforeUpdate</event>
  </target>
  ...
```

Here the configuration is indicating that the matching algorithm should be applied to resources of type Patient. The match engine makes no assumption about the target resource, match targets can be resources of type Patient, Person, Organization, Place, UserEntity, DeviceEntity, etc.

### Blocking Stage Configuration

The blocking stage is configured using one or more \<blocking> elements, blocking elements are structured [HDSI format ](../developers/service-apis/health-data-service-interface-hdsi/hdsi-query-syntax/)queries which are executed against the configured persistence layer. Blocking can be configured as illustrated:

```markup
  <!-- Patient which have same MRN -->
  <blocking maxResults="100">
    <filter>identifier[MRN].value=$input.identifier[MRN].value</filter>
    <filter>extension[http://santedb.org/extensions/core/detectedIssue]=[]</filter>
  </blocking>
```

Here the blocking filter is stating it wants to consider any record in the database with a matching identifier from domain MRN (identifier\[MRN].value) matching the input value ($input) and it only wants to consider records which have no detectedIssues (i.e. have not been flagged by the data quality engine as having issues).

The blocking filter will initially request the data layer to load 100 results (after which roundtrips to the database will be required).

#### Additional Blocking Filters

You can specify an infinite number of blocking filters to be run. Each resultset is either UNION (OR) or INTERSECT (and) with the previous. For example, the following configuration:

```markup
  <!-- Patient which have same MRN -->
  <blocking maxResults="100">
    <filter>identifier[MRN].value=$input.identifier[MRN].value</filter>
    <filter>extension[http://santedb.org/extensions/core/detectedIssue]=[]</filter>
  </blocking>
  <!-- Patient which have same HIN-->
  <blocking op="or" maxResults="100">
    <filter>identifier[HIN].value=$input.identifier[HIN].value</filter>
    <filter>extension[http://santedb.org/extensions/core/detectedIssue]=[]</filter>
  </blocking>
  <!-- Patients with same name and born within 2 y and name is within 2 corrections of one another -->
  <blocking op="or" maxResults="100">
    <filter>dateOfBirth=:(date_diff|$input.dateOfBirth)&lt;2y</filter>
    <filter>name.component[Given].value=:(levenshtein|$input.name.component[Given].value)&lt;2</filter>
    <filter>address.component[State].value=$input.address.component[State].value</filter>
    <filter>extension[http://santedb.org/extensions/core/detectedIssue]=[]</filter>
  </blocking>
```

Will perform three queries against the database for candidate records:

1. All patients where identifier MRN matches the $input
2. UNION all patients where identifier HIN matches the $input value
3. UNION all patients which were:
   1. Born within 2 years of the input record
   2. Have a given name no more than 2 characters different than the candidate
   3. Live in the same state
   4. Don't have any data quality issues

### Scoring Stage Configuration

Scoring is configured in the \<scoring> section which applies to one or more attributes from the records loaded during the blocking phase. A simple example provided below instructs the patient's gender to be scored.

```markup
<scoring>
    <attribute property="genderConcept" u="0.5" m="0.75" whenNull="nonmatch" required="true">
      <assert op="eq"/>
    </attribute>
```

| Attribute | Type       | Description                                                                                             |
| --------- | ---------- | ------------------------------------------------------------------------------------------------------- |
| property  | xs:string  | The property path on both objects to consider                                                           |
| u         | xs:decimal | The u probability (the probability the property will agree by pure coincidence)                         |
| m         | xs:decimal | The m probability (the probability a matching value indicates a match)                                  |
| whenNull  | xs:enum    | The behavior the engine should take when the value is null in either record A or record B               |
| required  | xs:boolean | Whether the attribute assertions need to evaluate (or be handled by whenNull) for matching to continue. |

Here the configuration is instructing the matching engine to consider genderConcept of record A (new object) and record B (the existing object), and the values must exactly match.

#### Handling Missing Data

There can occur instances of either the inbound record or the source records from the database which are missing the specified attribute. When this is the case the attribute's `whenNull` attribute controls the behavior of the evaluation of that attribute. The behaviors are:

| @whenNull  | Description                                                                                                                                                                                             |
| ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| match      | <p>When the value is null in A or B, treat the attribute as a "match" <br>(i.e. assume the missing data matches)</p>                                                                                    |
| nonmatch   | <p>When the value is null in either A or B, treat the attribute as a non-match</p><p>(i.e. assume the missing data would not match)</p>                                                                 |
| ignore     | <p>When the value is null in A or B, don't evaluate the attribute. <br>(i.e. neither the non-match or match scores should be considered) </p>                                                           |
| disqualify | <p>When the value is null in A or B disqualify the entire record from consideration</p><p>(i.e. it doesn't matter what the other attribute scores are, the record is considered </p><p>not a match)</p> |

#### Transforming Data

You can instruct the matching classification stage to transform the data on record A and record B prior to evaluating an assertion. This is done with a transform, for example, if we wanted to only compare the week of birth we could use this configuration:

```markup
    <attribute property="dateOfBirth" u="0.019" m="0.85" whenNull="nonmatch" required="true" >
      <assert op="eq">
        <transform name="date_extract">
          <args>
            <string>w</string>
          </args>
        </transform>
      </assert>     
    </attribute>
```

The date\_extract is applied to both records and then the assertion of "eq" is applied. The following data transforms are available in SanteDB.

| Transform            | Applies        | Action                                                                                                                                                                 |
| -------------------- | -------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| addresspart\_extract | Entity Address | Extracts a portion of an address for consideration                                                                                                                     |
| date\_difference     | Date           | Extracts the difference (in weeks, months, years, etc.) between the A record and B record.                                                                             |
| date\_extract        | Date           | Extracts a portion of the date from both records.                                                                                                                      |
| name\_alias          | Entity Name    | Considers any of the configured aliases for the name meeting a particular threshold of relevance (i.e. Will = Bill is stronger than Tess = Theresa)                    |
| abs                  | Number         | Returns the absolute value of a number                                                                                                                                 |
| dmetaphone           | Text           | Returns the double metaphone code (with configured code length) from the input string                                                                                  |
| length               | Text           | Returns the length of text string                                                                                                                                      |
| levenshtein          | Text           | Returns the levenshtein string difference between the A and B values.                                                                                                  |
| sorensen\_dice       | Text           | Returns the Sorensen Dice coefficient of text content A and B values.                                                                                                  |
| jaro\_winkler        | Text           | Returns the Jaro-Winkler (with default threshold of 0.7) between A and B values.                                                                                       |
| metaphone            | Text           | Returns the metaphone phonetic code for the attribute                                                                                                                  |
| similarity           | Text           | Returns a %'age (based on levenshtein difference) of string A to string B (i.e. 80% similar or 90% similar)                                                            |
| soundex              | Text           | Extracts the soundex codification of the input values.                                                                                                                 |
| substr               | Text           | Extracts a portion of the input values                                                                                                                                 |
| tokenize             | Text           | Tokenizes the input string based on splitting characters, the tokenized values can then be transformed independently using any of the transforms listed in this table. |
| timespan\_extract    | TimeSpan       | Extracts a portion of a timespan such as minutes, hours, seconds.                                                                                                      |

#### Custom Transforms

Attribute transform algorithms can be implemented by creating a new implementation of either IUnaryDataTransformer or IBinaryDataTransformer.&#x20;

* IUnaryTrasnformer - Is applied to each input independently and the each value is then compared to each other using the assertion logic.
* IBinaryTransformer - Is applied to both inputs with a result being passed to the assertion.

The example below illustrates the implementation to the "similarity" transform

```csharp
    /// <summary>
    /// Represents a transform which reports the similarity
    /// </summary>
    public class SimilarityTransform : IBinaryDataTransformer
    {
        /// <summary>
        /// Gets the name of the transform
        /// </summary>
        public string Name => "similarity";

        /// <summary>
        /// Applies the filter
        /// </summary>
        public object Apply(object a, object b, params object[] parms)
        {
            if (a is String)
                return ((String)a).SimilarityTo((String)b);
            else if (a is IEnumerable aEnum && b is IEnumerable bEnum)
                return aEnum.OfType<String>().SelectMany(sa => bEnum.OfType<String>().Select(sb => sa.SimilarityTo(sb)));
            else
                throw new InvalidOperationException("Cannot process this transformation on this type of input");
        }
    }
```

Custom transforms can be implemented using any .NET language (C#, Pascal, Iron Python, Visual Basic, etc).

#### Chaining Transforms

Transforms can be chained, for example, if you want to extract the Given name and then compare levenshtein difference of a Patient's mother's name:

```markup
<attribute property="relationship[Mother].target.name" u="0.15" m="0.6" whenNull="ignore" required="false">
      <assert op="lte" value="2">
        <transform name="namepart_extract">
          <args>
            <string>Given</string>
          </args>
        </transform>
        <transform name="levenshtein"/>
      </assert>
    </attribute>
```

This configuration will consider the Mother's name (relationship\[Mother].target.name) and will extract (namepart\_extract) the Given name, then apply a levenshtein difference. The result must be less than or equal to 2 (op=lte value=2)

#### Conditional Evaluation

You can also instruct the matching engine to only run or consider an attribute if another attribute is populated. For example, we may want to consider the patient's City address only if the state matches:

```markup
   <attribute id="address.state" property="address" u="0.05" m="0.75" whenNull="nonmatch" required="true">
      <assert op="eq">
        <transform name="addresspart_extract">
          <args>
            <string>State</string>
          </args>
        </transform>
      </assert>
    </attribute>
    <!-- Same County - If on average a state has 30 counties the u = 0.033   -->
    <attribute id="address.county" property="address" u="0.033" m="0.8" whenNull="ignore" required="false">
      <when>
        <attribute ref="address.state" op="eq" value="true"/>
      </when>
      <assert op="eq">
        <transform name="addresspart_extract">
          <args>
            <string>City</string>
          </args>
        </transform>
      </assert>
    </attribute>
```

{% hint style="info" %}
Note: Since the property path for both attributes are the same (address) the scoring engine will consider these two properties related, and will execute them as pairs. For example, if a patient has both a VacationHome and a Home address this configuration will consider VacationHome as one address for both attributes and Home. If using **address.component\[State].value and address.component\[City].value** instead then the scoring algorithm would treat these as two different property paths.
{% endhint %}

#### Partial Scoring

It is possible to apply a partial score to a match attribute. The understand why this may be beneficial, consider the match attribute configuration based on the Double-Metaphone code of a patient's name:

```markup
<attribute property="name" u="0.15" m="0.6" whenNull="ignore" required="false">
      <assert op="eq">
        <transform name="namepart_extract">
          <args>
            <string>Given</string>
          </args>
        </transform>
        <transform name="dmetaphone"/>
      </assert>
    </attribute>
```

Under such a configuration, a patient with the name **Kimberly** may be compared to existing patients as illustrated in the table below:

| Name              | Gender | DOB        | Address          |
| ----------------- | ------ | ---------- | ---------------- |
| Kimberleigh Smith | F      | 1992-01-12 | 123 Main Street  |
| Kimberly Smith    | F      | 1992-01-15 | 321 Brant Street |
| Kimber Smith      | F      | 1992-01-10 | 222 West Street  |

When evaluating a match the a attribute configuration will generate the Double Metaphone code of **KMPR** for all of these records, even though the candidate being considered doesn't match. Here it may be important to configure a partial score based on the levenshtein string difference between the original names and applying the percentage of difference to the calculated match score.

```markup
<attribute property="name" u="0.15" m="0.6" whenNull="ignore" required="false">
      <assert op="eq">
        <transform name="namepart_extract">
          <args>
            <string>Given</string>
          </args>
        </transform>
        <transform name="dmetaphone"/>
      </assert>
      <partialWeight name="similarity">
        <transform name="namepart_extract" source="attribute">
          <args>
            <string>Given</string>
          </args>
        </transform>
      </partialWeight>
</attribute>
```

Here, the matching engine would alter the given scores for each of the patients under consideration:

| Name              | namepart\_extract | dmetaphone | assertion | similarity | Score                |
| ----------------- | ----------------- | ---------- | --------- | ---------- | -------------------- |
| Kimberleigh Smith | Kimberleigh       | KMPR       | PASS      | 0.429      | 42% of match score   |
| Kimberly Smith    | Kimberly          | KMPR       | PASS      | 1.0        | 100% of match score  |
| Kimber Smith      | Kimber            | KMPR       | PASS      | 0.715      | 71.5% of match score |

## Bulk / Batch Matching

Each data type which is registered in the [Master Data Management](data-storage-patterns/master-data-storage.md) pattern has a corresponding [Match Job](../operations/cdr-administration/santedb-administration-panel/system-administration/jobs.md) registered. This job resets the suspected ground truth using the following rules:

| Remove / Delete:                                                                              | Keep:                                                                                  |
| --------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------- |
| <ul><li>Suspected Client Links (MDM-Candidate links)</li><li>Automatic Master Links</li></ul> | <ul><li>Verified Ignore</li><li>Verified Matches</li><li>System Master Links</li></ul> |

After the suspected truth is cleared, the job will begin the process of re-matching the registered dataset for SanteDB. The matching process is multi-threaded, and designed to ensure that the machine on which the match process is as efficient as possible. To do this, the following pattern is used:

![](<../.gitbook/assets/image (444).png>)

The batch matching process registers 4 primary threads on the actively configured thread pool to control the match process:

* Gather Thread: This worker is responsible for querying data from the source dataset in 1,000 record batches. The rate at which the records are loaded will depend on the speed of the persistence layer (SanteDB 2.1.x or 2.3.x) as well as the disk performance of the storage technology.
* Match Thread: This worker is responsible for breaking the 1,000 record batches into smaller partitions of records (depending on CPU of host machine). The configured matching algorithm is then launched for each record in the batch on independent threads (i.e. matching is done concurrently on the host machine).&#x20;
* Writer Thread: Once the match thread workers have completed their matching task, the results are queued for the writer thread. The writer thread is responsible for committing the matches to the read/write database.&#x20;
* Monitor Thread: The monitoring thread is responsible for updating the status of the job.

The performance of the batch matching will depend on the speed of the host machine as well as the version of SanteDB that is being used.&#x20;

SanteSuite's community server  was used for testing in the following configuration:

* Application Server:&#x20;
  * 4 VCPU&#x20;
  * 4 GB RAM&#x20;
  * Non-persistent (ram-only) REDIS Cache
* Database Server:&#x20;
  * 12 VCPU&#x20;
  * 12 GB RAM&#x20;
  * RAID 1+0 SSD disk infrastructure (4+4 SSD)

The versions of SanteDB tested yielded the following results:

* Version < 2.1.160 of SanteDB: \~28,000 records per hour
* Version > 2.1.165 of SanteDB: \~50,000 records per hour
* Version 2.3.x of SanteDB (internal alpha): \~100,000 records per hour

{% hint style="info" %}
It is important to ensure that your host system is configured such that the thread pool (accessed through the Probes administrative panel) has at minimum, 5 available worker threads to complete batch matching.&#x20;
{% endhint %}
