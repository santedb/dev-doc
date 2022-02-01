# Filter Functions

Filter functions provided by the SanteSuite community are summarized on this page.&#x20;

## Core HDSI Filters

### Age

The `age` filter is used to express a filter based on the "age" of a timestamp at a particular date. Age can be passed with no parameters (indicating age at current date) or can be used with a parameter (indicating age at specified date).

```
:(age)value
:(age|yyyy-MM-dd)value
```

Where `value` is an ISO8601 duration format.

| Parameter | Opt      | Description                                                                               |
| --------- | -------- | ----------------------------------------------------------------------------------------- |
| dateOfAge | Optional | The date on which the age value should be evaluated.                                      |
| (return)  |          | The date difference between the filter field and the input parameter in ISO8601 duration. |

#### SQL Translations

| PostgreSQL  | Supported (since 2.1)          |
| ----------- | ------------------------------ |
| FirebirdSQL | Supported (since 2.1)          |
| SQLite      | Not Supported (see date\_diff) |

PostgreSQL

```
WHERE GREATEST(column::TIMESTAMP - COALESCE(@otherDate::TIMESTAMP, CURRENT_TIMESTAMP), 
      COALESCE(@otherDate::TIMESTAMP, CURRENT_TIMESTAMP) - column::TIMESTAMP) <operator> @value::INTERVAL
```

FirebirdSQL

```
WHERE ABS(DATEDIFF(millisecond, CAST(column AS TIMESTAMP), 
         COLESACE(CAST(@otherDate AS TIMESTAMP), CURRENT_TIMESTAMP)) <operator> @value
```

#### Examples

```
// Under 1 year at current date
dateOfBirth=:(age)<P1Y
// Over 2 years old on Jan 1 2022
dateOfBirth=:(age|2022-01-01)>P2Y
```

### Date Difference

The date difference function is enabled on PostgreSQL and FirebirdSQL ORM providers and require no additional configuration. The `value` is any HDSI operator and an ISO8601 duration.

```csharp
:(date_diff|otherDate)value
```

| Parameter  | Opt      | Description                                                                                                            |
| ---------- | -------- | ---------------------------------------------------------------------------------------------------------------------- |
| @otherDate | Required | The other date to compare to. This duration is translated to `TimeSpan` and the total seconds are used for comparison. |
| (return)   |          | The difference between the property and the otherDate in ISO8601 duration                                              |

#### SQL Translations

| PostgreSQL  | Supported (since 2.0) |
| ----------- | --------------------- |
| FirebirdSQL | Supported (since 2.0) |
| SQLite      | Supported (since 2.0) |

PostgreSQL

```
WHERE GREATEST(column::TIMESTAMP - @otherDate::TIMESTAMP, 
      @otherDate::TIMESTAMP - column::TIMESTAMP) <operator> @value::INTERVAL
```

FirebirdSQL

```
WHERE ABS(DATEDIFF(millisecond, CAST(column AS TIMESTAMP), 
         CAST(@otherDate AS TIMESTAMP)) <operator> @value
```

SQLite

```
WHERE ABS(column - @otherDate.Ticks) <operator> @value.Ticks
```

#### Examples

```csharp
// Born within 3 years of 1990
dateOfBirth=:(date_diff|1990)<3y
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

#### SQL Translations

| PostgreSQL  | Supported (since 2.0) |
| ----------- | --------------------- |
| FirebirdSQL | Supported (since 2.0) |
| SQLite      | Supported (since 2.0) |

PostgreSQL & FirebirdSQL

```
WHERE SUBSTRING(column FROM @start FOR @length) <operator>
       SUBSTRING(@value FROM @start FOR @length)
```

SQLite

```
WHERE substr(column, @start, @length) <operator> substr(@value, @start, @length)
```

#### Examples

```csharp
// Identifier where the first 5 digits match 12345
identifier.value=:(substr|0,5)12345
```

### Date Truncate

Truncates a full `DateTime` or `DateTimeOffset` object to only the precision specified.

```
:(date_trunc|[yMd])value
```

| Parameter | Opt      | Description                                                                                |
| --------- | -------- | ------------------------------------------------------------------------------------------ |
| precision | Required | <ul><li>y = Year portion</li><li>M = Year + Month</li><li>d = Year + Month + Day</li></ul> |
| (return)  |          | A `DateTime` or `DateTimeOffset` truncated to only the portion specified.                  |

#### SQL Translations

| PostgreSQL  | Supported (since 2.2) |
| ----------- | --------------------- |
| FirebirdSQL | Supported (since 2.2) |
| SQLite      | Not Supported         |

PostgreSQL / FirebirdSQL&#x20;

```
WHERE column BETWEEN @minDate AND @maxDate
```

`@minDate` and `@maxDate` are computed in .NET based on precision where:

| Precision | @minDate                                    | @maxDate                                                                  |
| --------- | ------------------------------------------- | ------------------------------------------------------------------------- |
| Year      | `new DateTime(value.Year, 01, 01)`          | `new DateTime(value.Year, 12, 31)`                                        |
| Month     | `new DateTime(value.Year, value.Month, 01)` | `new DateTime(value.Year, value.Month, DateTime.DaysInMonth(value.Month)` |
| Day       | `value.Date`                                | `value.Date`                                                              |

## SanteMatch Filters

### Approximate Match

Approximate matching is enabled when the SanteDB matcher plugin is enabled in the configuration for the dCDR or iCDR. The approximate matching function will use a combination of pattern, phonetic, and string difference functions to determine matching based on the configuration of the server running the query.

```csharp
:(approx|otherString)
```

| Parameter   | Opt      | Description                                                                         |
| ----------- | -------- | ----------------------------------------------------------------------------------- |
| otherString | Required | The other string to compare approximation to                                        |
| (return)    |          | True if the server determines the property is approximately the same as otherString |

#### SQL Translations / Support

| PostgreSQL  | Supported (since 2.0) |
| ----------- | --------------------- |
| FirebirdSQL | Supported (since 2.0) |
| SQLite      | Not Supported         |

#### Examples

Filter for a name which sounds like, is about the same as, or minor typo's from JIHN (i.e. match JOHN, JOHNNY, JON, etc.).

```csharp
name.component.value=:(approx|JIHN)
```

### Sounds Like

Uses the configured phonetic algorithm to determine whether the supplied string sounds like the stored property value. The algorithm, if not specified by the implementer, is the discretion of the implementer of the server plugin.

```csharp
:(soundslike|otherString,[algorithm])
```

| Parameter   | Opt      | Description                                                        |
| ----------- | -------- | ------------------------------------------------------------------ |
| otherString | Required | The other string to compare                                        |
| algorithm   | Optional | Dictates the algorithm to use (soundex, metaphone, dmetaphone)     |
| (return)    |          | True if the server determines the property sounds like otherString |

#### SQL Translations / Support

| PostgreSQL  | Supported (since 2.0)                                                                                    |
| ----------- | -------------------------------------------------------------------------------------------------------- |
| FirebirdSQL | Not Supported                                                                                            |
| SQLite      | Supported (since 2.0 - requires SQLite [Soundex ](https://sqlite.org/lang\_corefunc.html#soundex)option) |

#### Examples

To filter for patients who have a name which sounds like Tyler (i.e. match Tyler, Tiler, etc.)

```csharp
name.component.value=:(soundexlike|TYLER)
```

### Phonetic Difference

The phonetic difference function is used to compare the difference in phonetic codes between two values. This function by default uses the SOUNDEX algorithm and then performs a LEVENSHTEIN function against the result.

```csharp
:(phonetic_diff|otherString,[algorithm])value
```

| Parameter   | Opt      | Description                                                    |
| ----------- | -------- | -------------------------------------------------------------- |
| otherString | Required | The other string to compare                                    |
| algorithm   | Optional | Dictates the algorithm to use (soundex, metaphone, dmetaphone) |
| (return)    |          | The difference (0 - 4) in soundex codes                        |

#### SQL Translations / Support

| PostgreSQL  | Supported (since 2.1) |
| ----------- | --------------------- |
| FirebirdSQL | Not Supported         |
| SQLite      | Not Supported         |

### Soundex Comparison&#x20;

The soundex comparison is used to compare the difference in SOUNDEX codes of each input.

```
:(soundex)OTHER
```

#### SQL Translations / Support

| PostgreSQL  | Supported (since 2.0)                                                                                    |
| ----------- | -------------------------------------------------------------------------------------------------------- |
| FirebirdSQL | Not Supported                                                                                            |
| SQLite      | Supported (since 2.0 - requires SQLite [Soundex ](https://sqlite.org/lang\_corefunc.html#soundex)option) |

### Metaphone Comparison

The metaphone comparison is used to compare the values based on their metaphone code. Metaphone filter takes an optional length specifier.

```
:(metaphone)OTHER
:(metaphone|3)OTHER
```

#### SQL Translations / Support

| PostgreSQL  | Supported (since 2.0)                                                                        |
| ----------- | -------------------------------------------------------------------------------------------- |
| FirebirdSQL | Not Supported                                                                                |
| SQLite      | Supported (since 2.0 - requires SQLite [spellfix plugin](https://sqlite.org/spellfix1.html)) |

### Double Metaphone Comparison

The double metaphone comparison is used to compare values based on the double metaphone code.

```
:(dmetaphone)OTHER
```

#### SQL Translations / Support

| PostgreSQL  | Supported (since 2.0) |
| ----------- | --------------------- |
| FirebirdSQL | Not Supported         |
| SQLite      | Not Supported         |

### Levenshtein Difference&#x20;

The levenshtein difference is used to compute the difference in edit distance between the source and input.

```
:(levenshtein|OTHER)<3
```

{% hint style="info" %}
Using the `levenshtein` function has a performance penalty in that the database tables storing the values (identifiers, addresses, etc.) needs to be sequentially scanned. If you can, consider using  `similarity_lev` which can uses PostgreSQL's trigram index (see `similarity` extension).
{% endhint %}

#### SQL Translations / Support

| PostgreSQL  | Supported (since 2.0)                                                                        |
| ----------- | -------------------------------------------------------------------------------------------- |
| FirebirdSQL | Not Supported                                                                                |
| SQLite      | Supported (since 2.0 - requires SQLite [spellfix plugin](https://sqlite.org/spellfix1.html)) |

### Similarity

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

#### SQL Translations / Support

| PostgreSQL  | Supported (since 2.2) |
| ----------- | --------------------- |
| FirebirdSQL | Not Supported         |
| SQLite      | Not Supported         |

### Similarity + Levenshtein

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

#### SQL Translations / Support

| PostgreSQL  | Supported (since 2.2) |
| ----------- | --------------------- |
| FirebirdSQL | Not Supported         |
| SQLite      | Not Supported         |

## Custom Filter Functions

Implementers can write custom filter functions by implementing the following interfaces:

* [IQueryExtensionFilter](http://santesuite.org/assets/doc/net/html/T\_SanteDB\_Core\_Model\_Query\_IQueryFilterExtension.htm) interface which maps and composes the HDSI query expression to/from a .NET Expression tree&#x20;
* Implementing a [.NET Extension Method](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/extension-methods) which allows the HDSI filter to be exposed in a .NET LINQ Expression (and which is used to evaluate the HDSI filter on .NET objects in memory)
* Implementing [IDbFilterFunction ](http://santesuite.org/assets/doc/net/html/Methods\_T\_SanteDB\_OrmLite\_Providers\_IDbFilterFunction.htm)interface for each persistence interface. This class translates the HDSI Query and LINQ extension into SQL for the appropriate platform.
