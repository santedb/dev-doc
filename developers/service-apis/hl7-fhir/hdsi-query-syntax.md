# HDSI Query Syntax

Both the HDSI and AMI use a general purpose query syntax which provide methods for matching records within the database on those interfaces. The HDSI query syntax is mapped to the RIM objects (wire format) returned by those APIs.

The HDSI query syntax is translated from HTTP query headers to LINQ expression trees and then used within the SanteDB iCDR and dCDR instances where needed (running business rules, filtering lists, querying against the database).

{% hint style="info" %}
When passing HDSI queries over HTTP you must URL encode them. The examples here are not URL encoded and only suitable in matching and care planning rules.
{% endhint %}

## Property Paths

In general an HDSI query is executed using parameters found in the object which is being queried. For example, an HDSI query for all patients named TEST would be:

```
name.component.value=TEST
```

This query is translated into a .NET expression tree roughly equivalent to

```csharp
o => o.Names.Any(name => name.Component.Any(component => component.Value == "TEST"))
```

The properties are traversed using dotted notation matching the property names in the returned object as illustrated below.

![](<../../../.gitbook/assets/image (159).png>)

## And/Or Semantics

By default all filters passed in an HDSI query string are AND unless the property path is the same, in which case multiples are treated as OR. For example, to find patients with any name component of either JOHN or SMITH

```csharp
name.component.value=JOHN&name.component.value=SMITH
```

However, if guards are applied, we can execute given name JOHN and family name SMITH

```csharp
name.component[Given].value=JOHN&name.component[Family].value=SMITH
```

If we wanted to query for given name of JOHN or JOHNNY and family name of SMITH

```csharp
name.component[Given].value=JOHN&name.component[Given].value=JOHNNY&name.component[Family].value=SMITH
```

## Operators

Operators allow for the filtering of values based on equality, negation, etc. The operators for HDSI query syntax are listed below:

| Operation             | Operator | Example                     |
| --------------------- | -------- | --------------------------- |
| Equal                 | =        | name.component.value=JOHN   |
| Not Equal             | =!       | name.component.value=!JOHN  |
| Less Than             | =<       | dateOfBirth=<2020-01-01     |
| Less Than or Equal    | =<=      | dateOfBirth=<=2020-01-01    |
| Greater Than          | =>       | dateOfBirth=>2020-01-01     |
| Greater Than or Equal | =>=      | dateOfBirth=>=2020-01-01    |
| About Equal (Pattern) | =\~      | name.component.value=\~JO\* |
| Starts With           | =^       | name.component.value=^JO    |
| Ends With             | =$       | name.componentvalue=$HN     |

## Collection Guards

By default any filter which is applied to a property which is a collection (identifiers, name, addresses, etc.) is filtered as ANY. The following example illustrates a match where any identifier of a patient equals 123-234-234:

```csharp
identifier.value=123-234-234
```

In order to specify a particular instance on a traversal a guard is applied, guards are applied using square brackets and the code mnemonic of the classifier you want to guard on. For example, if we wanted only patients having an SSN of 123-234-234:

```csharp
identifier[SSN].value=123-234-234
```

Classifiers on properties will depend on the type of property being filtered, a common list of properties and their classifiers are included below.

| Type                     | Classifier          | Example                                  |
| ------------------------ | ------------------- | ---------------------------------------- |
| Addresses                | Address Use         | address\[HomeAddress].component.value=ON |
| Names                    | Name Use            | name\[Legal].component.value=SMITH       |
| Identifiers              | Identifier Assigner | identifier\[SSN].value=123-123-123       |
| Telecoms                 | Telecom Use         | telecom\[WorkPlace].value=304-043-2039   |
| Relationships            | Relationship Type   | relationship\[Mother].target=UUID        |
| Participations           | Participation Role  | participation\[RecordTarget].player=UUID |
| Name / Address Component | Component Type      | name.component\[Given].value=JOHN        |

If using multiple classifiers you can either represent them individually

```csharp
name[Legal].component.value=SMITH&name[OfficialRecord].component.value=SMITH
```

However this is not recommended as the query builder will create two clauses, the query above roughly translates to:

```csharp
o => o.Names.Where(
        guard => guard.NameUse.Mnemonic == "Legal"
     ).Any(
        name => name.Component.Any(
           component => component.Value == "SMITH"))
     || o.Names.Where(
        guard => guard.NameUse.Mnemonic == "OfficialRecord")
        .Any(
           name => name.Component.Any(
              component => component.Value == "SMITH"))
```

Instead you can combine the guards:

```csharp
name[Legal|OfficialRecord].component.value=SMITH
```

Which translates to a reduced LINQ expression:

```csharp
o => o.Names.Where(
          guard => guard.NameUse.Mnemonic == "Legal" 
                || guard.NameUse.Mnemonic == "OfficialRecord")
      .Any(
          name => name.Component.Any(
               component => component.Value == "SMITH"))
```

## Casting

Sometimes an occasion arises where you wish to execute a sub-filter on a property which is of the wrong type. For example, if we wanted to filter for patients who have Mother with a date of birth before 1960, we would expect this query to work:

```csharp
relationship[Mother].target.dateOfBirth=<1960
```

However, looking at the traversal for **target** on the **EntityRelationship** class, the type is of **Entity** rather than a **Person**. Entity does not have a **dateOfBirth** , we need to tell the query engine that we want to further restrict the target to be a Person, this is done with the CAST operator:

```csharp
relationship[Mother].target@Person.dateOfBirth=<1960
```

## Coalesce

Sometimes a traversal path may not have a value, this can cause issues when the iCDR attempts to execute filters against in-memory objects such as in the care planner or matching engine. In these scenarios you can use the coalesce operator (also known as the "Elvis" operator). This operator does null-safe traversal, for example, to match a patient with a gender code which may or may not be present:

```csharp
genderConcept?.mnemonic=Male
```

## Variables

Variables are either defined by the user (for example, in the data retention service) or by the host context (such as `$index` in the CDSS for repeated actions, or `$input` in the matcher for the inbound record).&#x20;

Variables may be referenced as the value, for example, if a `$mothersBirth` variable was defined in a retention policy, it could be used in the filter as:

```
relationship[Mother].target@Person.dateOfBirth=<$mothersBirth
```

Variables can also be used as the root of another HDSI expression, for example, comparing the city in which an `$input` patient lives.

```
address.component[City].value=$input.address.component[City].value
```

## Extension Functions

The default matching operations may be extended via SanteDB's query extension methods. These methods allow for custom matching parameters. These extension functions are enumerated below (with a discussion on which plugins must be enabled to activate them).

Functions are applied in the format:

```csharp
property=:(extension|parameter1,parameter2)value
```

### Date Difference

The date difference function is enabled on PostgreSQL and FirebirdSQL ORM providers and require no additional configuration.

```csharp
:(date_diff|otherDate)value
```

| Parameter | Opt      | Description                                           |
| --------- | -------- | ----------------------------------------------------- |
| otherDate | Required | The other date to compare to                          |
| (return)  |          | The difference between the property and the otherDate |

For example, to filter for patients born within 3 years of 1990

```csharp
dateOfBirth=:(date_diff|1990)<3y
```

### Date Component Extract

The date extract component extracts a part of the date compares with the property.

```csharp
:(date_extract|month/year/day/week/hour/minute)value
```

| Parameter | Opt      | Description                                              |
| --------- | -------- | -------------------------------------------------------- |
| datePart  | Required | The part of the date to extract (year, month, day, etc.) |
| (return)  |          | The extracted part of the date                           |

For example, to filter for patients born during the month of May

```csharp
dateOfBirth=:(date_extract|month)5
```

### Substring

Extracts a portion of a string and matches it with the provided value.

```csharp
:(substr|start,[length])value
```

| Parameter | Opt      | Description                         |
| --------- | -------- | ----------------------------------- |
| start     | Required | The starting position in the string |
| length    | Optional | The length to extract               |
| (return)  |          | The extracted part of the string    |

For example, to filter for patients who have an identifier where the first 5 digits match 12345.

```csharp
identifier.value=:(substr|0,5)12345
```

### Approximate Match

Approximate matching is enabled when the SanteDB matcher plugin is enabled in the configuration for the dCDR or iCDR. The approximate matching function will use a combination of pattern, phonetic, and string difference functions to determine matching.

```csharp
:(approx|otherString)
```

| Parameter   | Opt      | Description                                                                         |
| ----------- | -------- | ----------------------------------------------------------------------------------- |
| otherString | Required | The other string to compare approximation to                                        |
| (return)    |          | True if the server determines the property is approximately the same as otherString |

For example, to filter for patients who have a name which sounds like, is about the same as, or minor typo's from JIHN (i.e. match JOHN, JOHNNY, JON, etc.).

```csharp
name.component.value=:(approx|JIHN)
```

### Sounds Like (santedb-match plugin)

Uses the configured phonetic algorithm to determine whether the supplied string sounds like the stored property value.

```csharp
:(soundslike|otherString,[algorithm])
```

| Parameter   | Opt      | Description                                                        |
| ----------- | -------- | ------------------------------------------------------------------ |
| otherString | Required | The other string to compare                                        |
| algorithm   | Optional | Dictates the algorithm to use (soundex, metaphone, dmetaphone)     |
| (return)    |          | True if the server determines the property sounds like otherString |

For example, to filter for patients who have a name which sounds like Tyler (i.e. match Tyler, Tiler, etc.)

```csharp
name.component.value=:(soundexlike|TYLER)
```

### Phonetic Difference (santedb-match plugin)

The phonetic difference function is used to compare the difference in phonetic codes between two values. This function by default uses the SOUNDEX algorithm and then performs a LEVENSHTEIN function against the result.

```csharp
:(phonetic_diff|otherString,[algorithm])value
```

| Parameter   | Opt      | Description                                                    |
| ----------- | -------- | -------------------------------------------------------------- |
| otherString | Required | The other string to compare                                    |
| algorithm   | Optional | Dictates the algorithm to use (soundex, metaphone, dmetaphone) |
| (return)    |          | The difference (0 - 4) in soundex codes                        |

### Soundex Comparison (santedb-match plugin)

The soundex comparison is used to compare the difference in SOUNDEX codes of each input.

```
:(soundex)OTHER
```

### Metaphone Comparison (santedb-match plugin)

The metaphone comparison is used to compare the values based on their metaphone code. Metaphone filter takes an optional length specifier.

```
:(metaphone)OTHER
:(metaphone|3)OTHER
```

### Double Metaphone Comparison (santedb-match plugin)

The double metaphone comparison is used to compare values based on the double metaphone code.

```
:(dmetaphone)OTHER
```

### Levenshtein Difference (santedb-match plugin)

The levenshtein difference is used to compute the difference in edit distance between the source and input.

```
:(levenshtein|OTHER)<3
```

{% hint style="info" %}
Using the `levenshtein` function has a performance penalty in that the database tables storing the values (identifiers, addresses, etc.) needs to be sequentially scanned. If you can, consider using  `similarity_lev` which can uses PostgreSQL's trigram index (see `similarity` extension).
{% endhint %}

### Similarity (santedb-match plugin)

The similarity function will use the database's string matching similarity functionality to perform an indexed match (in PostgreSQL the similarity operator used). For example, to compare similarity of given names > 0.8 from SMITH

```
name.component[Family].value=:(similarity|SMITH)>0.8
```

{% hint style="info" %}
When using PostgreSQL the `:(similarity)` filter function will be translated into an optimized lookup of `column % 'SMITH' AND similarity(column, 'SMITH') > 0.8` . It is therefore important to properly set the default (used by the `%` operator) via:&#x20;

```sql
ALTER DATABASE santedb SET pg_trgm.word_similarity_threshold = 0.6;
```
{% endhint %}

### Similarity + Levenshtein (santedb-match plugin)

The `similarity_lev` filter acts similar to the similarity in that it uses the underlying database technology's GIN indexing to perform a similarity, however the final result is run through the `levenshtein` function.&#x20;

```
identifier[SSN].value=:(similarity_lev|304-304-3049)<3
```

Would be queried in PostgreSQL as:

```
WHERE id_val % '304-304-3049' AND levenshtein(id_val, '304-304-3049') < 3
```

This method should be used over similarity when:

* The strings being compared require an exact number of modifications to pass the filter (like identifiers accounting for type-o's)
* The use case has too many values for a plain levenshtein and a pre-index of similarity is preferred.

Implementers should note that the default similarity threshold will impact what is passed to levenshtein and the database will need be tuned based on the implementation specific data. For example, if using Canadian Social Insurance Numbers, with a desired levenshtein test of 5 then it would best to set `word_similarity_threshold` to 0.4 since SIN numbers with 5 edits would be represent a 60% difference in source strings.

## Control Parameters

HDSI query control parameters are prefixed with an underscore. These query parameters are not mapped to the internal data structures of the RIM for filtering, and are intended, to provide control over how the result set is returned.

| `_count`   | number             | Controls the number of records which are returned in the result set.                                  |
| ---------- | ------------------ | ----------------------------------------------------------------------------------------------------- |
| `_offset`  | number             | Controls the offset of the first record to be returned in the result set.                             |
| `_orderBy` | field:\[asc\|desc] | Controls the ordering of results in the result set.                                                   |
| `_any`     | string             | Initiates a free text search (or rather, allows the server to control how the result set is queried). |

## Freetext Search

The `_any` parameter in a search allows clients to execute a filter on any data in the requested resource. The behavior of the `_any` parameter depends on the persistence layer and how the [Broken link](broken-reference "mention") has been configured.

* On PostgreSQL this search uses the `tsvector` type to execute web search queries.
* On SQLite (before version 2.3 of the dCDR) the search uses a simple keyword search. Integration of the Lucene engine is being developed for version 2.3 of the dCDR
* On Firebird the search maps to a query on `name.component.value` or `address.component.value` or `identifier.value`.

### PostgreSQL tsvector Search

If configured, the iCDR running on PostgreSQL will use the [PostgreSQL FreeText](https://www.postgresql.org/docs/12/textsearch.html) search engine. Searches can be executed as a simple web search. For example to match based on name, address, identifier or telecom of Jim and Smith:

```
_any=Jim Smith
```

Additionally simple logic can be applied via and/or:

```
_any='Jim Smith' and 'Beamsville ON' and 'FHR-304'
```

## Performance Tips

When writing your HDSI queries, you can ensure that you have higher performance by structuring your queries in a particular way. Some recommendations:

1. Use Guards: Whenever possible use guard conditions, this reduces the records to be filtered by the database system and (if you've partitioned tables) can dictate particular partitions to use.
2. Combine Guard Conditions: You can combine guard conditions as illustrated above, this ensures that results are filtered with one EXISTS condition in the database rather than multiple
3. Special Indexing: You can (and should) apply additional indexing to your SanteDB database to take advantage of common functions and queries. For example, if you often use the SOUNDEX algorithm to search for addresses, you might want to create an index like: \
   **CREATE INDEX addr\_cmp\_val\_soundex\_idx ON addr\_cmp\_val\_tbl(SOUNDEX(val));**
4. Partition Tables: You can partition collection tables based on their classifiers , this can make it easier for the database system to filter data based on classifiers. There is an partitioning script in the SQL\ directory of your iCDR installation folder. This sets up partitions for the entity relationship and act participations.

