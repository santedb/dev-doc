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

![](<../../../../.gitbook/assets/image (159).png>)

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

| Operation             | Operator       | Example                                                           |
| --------------------- | -------------- | ----------------------------------------------------------------- |
| Equal                 | `=` or `eq`    | name.component.value=JOHN                                         |
| Not Equal             | `=!` or `ne`   | <p>name.component.value=!JOHN<br>name.component.value=neJOHN</p>  |
| Less Than             | `=<` or `lt`   | <p>dateOfBirth=&#x3C;2020-01-01<br>dateOfBirth=lt2020-01-01</p>   |
| Less Than or Equal    | `=<=` or `lte` | <p>dateOfBirth=&#x3C;=2020-01-01<br>dateOfBirth=lte2020-01-01</p> |
| Greater Than          | `=>` or `gt`   | <p>dateOfBirth=>2020-01-01<br>dateOfBirth=gt2020-01-01</p>        |
| Greater Than or Equal | `=>=` or `gte` | <p>dateOfBirth=>=2020-01-01<br>dateOfBirth=gte2020-01-01</p>      |
| About Equal (Pattern) | `=~` or `ap`   | <p>name.component.value=~JO*<br>name.component.value=apJO*</p>    |
| Starts With           | =^             | name.component.value=^JO                                          |
| Ends With             | =$             | name.componentvalue=$HN                                           |

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

## Complex Guards

{% hint style="info" %}
This section documents a feature that is only available in SanteDB v3.0 or later
{% endhint %}

Guards can also contain complex expressions. Complex expressions in a guard are triggered by using the `=` sign in the guard. For example, to guard on a telecom address whose use is `Home` and type is an e-mail:

```
telecom[use.mnemonic=Home&amp;type.mnemonic=Internet].value=bob@bob.com
```

{% hint style="warning" %}
When submitting the request via a string or via HTTP directly the `=` in the guard expression must be URL escaped value of `%3d`
{% endhint %}

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

### Built-In Variables

The following variables are available when using the HDSI query syntax in any context.

| Variable | Type           | Description                                                       |
| -------- | -------------- | ----------------------------------------------------------------- |
| `$now`   | DateTimeOffset | The current timestamp on the iCDR or dCDR sever.                  |
| `$today` | DateTime       | The current date (year, month and day) on the iCDR or dCDR server |

### Matching Variables

When using the SanteDB matching engine the HDSI query syntax is extended to include additional variables.

| Variable | Type   | Description                                      |
| -------- | ------ | ------------------------------------------------ |
| `$input` | Entity | The entity which is attempting to be registered. |

### CDSS Variables

When evaluating HDSI expressions in the CDSS engine the following additional variables are exposed.

| Variable      | Type    | Description                                                                                                                                                               |
| ------------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `$index`      | Integer | When the `repeat` clause is specified on a rule, this represents the current index of the repetition                                                                      |
| `$background` | Boolean | When true, indicates that the CDSS rule is being called as part of a background process, when false indicates that the CDSS rule is being executed in the user interface. |

## Extension Functions

The default matching operations may be extended via SanteDB's query extension methods. These methods allow for custom matching parameters. These extension functions are enumerated below (with a discussion on which plugins must be enabled to activate them).

Functions are applied in the format:

```csharp
property=:(extension|parameter1,parameter2)value
```

See: [filter-functions.md](filter-functions.md "mention") for more information on filter functions.

## Control Parameters

HDSI query control parameters are prefixed with an underscore. These query parameters are not mapped to the internal data structures of the RIM for filtering, and are intended, to provide control over how the result set is returned.

| `_count`        | number             | Controls the number of records which are returned in the result set.                                                                                                          |
| --------------- | ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `_offset`       | number             | Controls the offset of the first record to be returned in the result set.                                                                                                     |
| `_orderBy`      | field:\[asc\|desc] | Controls the ordering of results in the result set.                                                                                                                           |
| `_any`          | string             | Initiates a free text search (or rather, allows the server to control how the result set is queried).                                                                         |
| `_includeTotal` | boolean            | True if the response should include the total count - this is used to allow callers to indicate that they don't want the API to perform the extra step of `COUNT` of results. |

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

