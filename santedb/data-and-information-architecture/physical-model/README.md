# Physical Model

In SanteDB, the physical model is used to express the concrete tables which are created in a SQL based RDBMS to store data on a physical media (disk). Implementers of new SQL based persistence services should try to re-use these mappings in their expression to the physical model.&#x20;

SanteDB uses the [ORM Lite](https://github.com/santedb/santedb-orm) data mapping technology, and the `SanteDB.Persistence.Data.Ado` assembly contains the ORM lite physical model classes.

{% hint style="info" %}
Version 2.5 of SanteDB is undergoing a major code refactor. The physical model classes in the 2.5.x series of SanteDB will reside in the `SanteDB.Persistence.Data` assembly.
{% endhint %}

\
Data Providers


SanteDB includes an implementation of a persistence layer which includes support for generic ADO based databases. This provider uses the ADO.NET wrapper to invoke necessary functions and select data from tables. In order to leverage the ADO.NET persistence service, the ADO.NET provider must support:

* SQL92 syntax&#x20;
* Limit and offset queries in the form of `SELECT FOO FROM BAR OFFSET x LIMIT y`
* Invoke of Stored Procedures and Functions or equivalent C# logic which implements the functions
* Pooled and thread-safe access to the underlying disk structure.

Currently SanteDB iCDR works with the following OrmLite data providers:

| **Database System**   | **Invariant** |
| --------------------- | ------------- |
| PostgreSQL 9.4 – 10.0 | npgsql        |
| FirebirdSQL 3.0       | FirebirdSQL   |
| SQLite 3.3            | Sqlite        |

&#x20;Regardless of the RDBMS system feeding the ADO provider, it must follow the schema specified in this section.

### Implementing new Data Providers

To implement a new ADO.NET based data provider, implementers will need to:

1. Write an ORM Lite `IDbProvider` instance (see an example of the [FirebirdSQL provider](https://github.com/santedb/santedb-orm/blob/master/SanteDB.OrmLite/Providers/Firebird/FirebirdSQLProvider.cs))
2. Write an ORM Lite `IDbConfigurationProvider` instance (see an example of the [FirebirdSQL Configuration provider](https://github.com/santedb/santedb-orm/blob/master/SanteDB.OrmLite/Providers/Firebird/FirebirdSQLConfigurationProvider.cs))
3. The DDL and DML classes for the most recent SanteDB physical model (see an example of the [FirebirdSQL DDL files](https://github.com/santedb/santedb-server/tree/master/SanteDB.Persistence.Data.ADO/Data/SQL/FBSQL))
   * You should include these as embedded resources in your plugin
   * You should include all updates , translated to your SQL dialect as well
   * You should include your own provider's invariant in the header
4. Implementations of any supported extended functions (such as SOUNDEX, LEVENSHTEIN, etc.) as `IDbFilterFunction` implementations (see an example [FirebirdSQL String Matching Functions](https://github.com/santedb/santedb-orm/blob/master/SanteDB.OrmLite/Providers/Firebird/StrMatchFunctions.cs))

## Patching SQL Tables

See: [Database Patching ](../../../developers/extending-santesuite/extending-santedb/server-plugins/database-patching.md)article for information on patching SQL structures.

## Conventions

The physical schema of the ADO provider is designed such that many different ADO providers can support the data structures. Because of the limitations on some RDBMS systems, the ADO schema uses a short-hand for table names.&#x20;

### Suffixes

The following suffixes are placed on entities in the schema:

| Suffix   | Used For               | Example             |
| -------- | ---------------------- | ------------------- |
| \_TBL    | Tables                 | `ENT_VRSN_TBL`      |
| \_VW     | Views                  | `ENT_CUR_VRSN_VW`   |
| \_CDTBL  | Code Lookup Tables     | `ENT_REL_CLS_CDTBL` |
| \_SYSTBL | Internal System Tables | `PATCH_DB_SYSTBL`   |

### General Naming Conventions

Most tables in the SanteDB physical model carry common abbreviations of names. Because of the varied contributors some tables break these rules, however the general principal applies:

* Names less than four characters should be represented in full (example: `NAME` or `TAG`)
* Names which represent a classified object carry their classification, for example:
  * `OBS_TBL` => Observation Table
  * `SUB_ADM_TBL` => Substance Administration Table
* Association tables which exist only to link together two other tables should have `ASSOC` in their name
* Longer table names are usually acronyms:
  * `CD_TBL` => **C**oncept **D**efinition Table&#x20;
  * `CS_TBL` => **C**ode **S**ystem Table
* Table and columns should remove vowels where the removal of vowels do no interfere with understanding the meaning of the column or table:
  * `ENT_TBL` => Entity Table
  * `CLS_CD_ID` => **Cl**a**s**s **C**oncept **D**efinition ID

### Inherited Tables

Tables which represent an inheritance are created as discrete tables. Each class in the hierarchy maps to one table in the schema and contain only the attributes of the class.&#x20;

As an example:

```csharp
// Entity 
public class Entity 
{
}

// Person IS A Entity
public class Person : Entity
{
}

// Patient IS A Person
public class Patient : Person
{
}
```

In the database schema this inheritance structure is represented as:

```sql
CREATE TABLE ENT_TBL
(
    ENT_ID UUID NOT NULL,
    ...
    CONSTRAINT PK_ENT_TBL PRIMARY KEY (ENT_ID)
);

-- PERSON IS A ENTITY
CREATE TABLE PSN_TBL
(
    ENT_ID UUID NOT NULL,
    ...
    CONSTRAINT PK_PSN_TBL PRIMARY KEY (ENT_ID)
    CONSTRAINT FK_PSN_ENT_TBL FOREIGN KEY (ENT_ID) REFERENCES ENT_TBL(ENT_ID)
);

-- PATIENT IS A PERSON
CREATE TABLE PAT_TBL
(
    ENT_ID UUID NOT NULL,
    ...
    CONSTRAINT PK_PAT_TBL PRIMARY KEY (ENT_ID)
    CONSTRAINT FK_PAT_PSN_TBL FOREIGN KEY (ENT_ID) REFERENCES PSN_TBL(ENT_ID)
);

```

{% hint style="info" %}
On a versioned database each class down the hierarchy should point to the version identification of the superclass rather than the identifier of the superclass - this is to track versioned changes to first class properties.
{% endhint %}

### Versioning

On persistence services which provide versioning (such as those in the iCDR) the tables can be split into two categories:

* Versioned Tables -> Acts, Entities and Concepts which track changes to data over time.
* Non-Versioned Tables -> Any other class which does not track changes over time.

{% hint style="info" %}
The legacy dCDR SQLite provider is un-versioned. This means all of its tables are not versioned.
{% endhint %}

Because version data is required for interfaces in the iCDR the structures are broken into a primary table and a versioning table, where:

* Primary Table: Contains the unchanging attributes of the object
* Version Table: Contains the attributes which may be changed on the object. This table contains:
  * Sequence Identification (used for tracking the order of versions)
  * Creation time and provenance (who created the version)
  * Obsolete time and provenance (who rendered this version obsolete)
  * Replaced version id (the version that this version replaces)

For example, `ENT_TBL` and `ENT_VRSN_TBL` are related in this manner:

```sql
CREATE TABLE ENT_TBL (
    ENT_ID UUID NOT NULL,
    -- NON-VERSIONED PROPERTIES
    CONSTRIANT PK_ENT_TBL PRIMARY KEY (ENT_ID)
);

-- ENTITY VERSION TABLE
CREATE TABLE ENT_VRSN_TBL (
    ENT_VRSN_ID UUID NOT NULL,
    VRSN_SEQ_ID BIGINT NOT NULL, -- THE VERSION SEQUENCEING IDENTIFIER
    ENT_ID UUID NOT NULL, -- THE ENTITY THIS VERSION APPLIES TO 
    CRT_UTC TIMESTAMP NOT NULL, -- THE TIME THE VERSION WAS CREATED
    CRT_PROV_ID UUID NOT NULL, -- THE PROVENANCE THAT CREATED THIS
    OBSLT_UTC TIMESTAMP, -- THE TIME THE VERSION IS NO LONGER VALID
    OBSLT_PROV_ID UUID, -- THE PROVENANCE OF WHAT OBSOLETED THIS
    RPLC_VRSN_ID UUID, -- THE REPLACED VERSION
    ... -- VERSIONED DATA FIELDS
    CONSTRAINT PK_ENT_VRSN_TBL PRIMARY KEY (ENT_VRSN_ID),
    CONSTRAINT FK_ENT_VRSN_ENT_TBL FOREIGN KEY (ENT_ID) REFERENCES ENT_TBL(ENT_ID),
    CONSTRAINT FK_ENT_VRSN_RPLC FOREIGN KEY (RPLC_VRSN_ID) REFERENCE ENT_VRSN_TBL(ENT_VRSN_ID)
);

CREATE UNIQUE INDEX ENT_VRSN_SEQ_UQ_IDX ON ENT_VRSN_TBL(VRSN_SEQ_ID);
```

Tables which are associated with a versioned entity should be linked to the primary key of the non-versioned portion of the data, and carry an `Effective Version Seq` and an `Obsolete Version Seq.` For example, identifiers for an entity:

```sql
-- ENTITY IDENTIFIER
CREATE TABLE ENT_ID_TBL (
    ENT_ID_ID UUID NOT NULL, -- SURROGATE PRIMARY KEY
    ENT_ID UUID NOT NULL, -- THE ENTITY TO WHICH THIS IDENTIFIER IS RELATED
    EFFT_VRSN_SEQ_ID BIGINT NOT NULL, -- THE VERSION OF THE ENTITY WHERE THIS ID WAS VALID
    OBSLT_VRSN_SEQ_ID BIGINT, -- THE VERSION OF THE ENTITY WHERE THIS ID IS NO LONGER VALID
    ... -- DATA FIELDS
    CONSTRAINT PK_ENT_ID_TBL PRIMARY KEY (ENT_ID_ID),
    CONSTRAINT FK_ENT_ID_ENT_TBL FOREIGN KEY (ENT_ID) REFERENCES ENT_TBL(ENT_ID),
    CONSTRAINT FK_ENT_ID_EFFT_VRSN_TBL FOREIGN KEY (EFFT_VRSN_SEQ_ID) REFERENCES ENT_VRSN_TBL(VRSN_SEQ_ID),
    CONSTRAINT FK_ENT_ID_OBSLT_VRSN_TBL FOREIGN KEY (OBSLT_VRSN_SEQ_ID) REFERENCES ENT_VRSN_TBL(VRSN_SEQ_ID)
) 
```
