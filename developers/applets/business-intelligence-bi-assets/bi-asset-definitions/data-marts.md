# Data Marts

{% hint style="info" %}
This page documents a feature in SanteDB version 3.0.
{% endhint %}

## Introduction

SanteDB's Business Intelligence services allow developers of SanteDB applets to define custom reports, queries, views and also (starting with Version 3.0) custom data marts.&#x20;

A data mart is replica of the primary SanteDB database whereby selective data is pre-pivoted, calculated and stored in a schema which is more suited for running reports. This makes writing reports easier and makes running reports faster. It also allows system administrators to host data for reporting purposes on another physical server instance.

The SanteDB BI data mart infrastructure allows for the extension and derivation of datamarts on one another. A data mart definition is defined in a new bi asset file with a `DatamartDefinition` element and contains:

* Metadata about the data mart definition including authors, and permissions to access the data mart.
* A data source registration which identifies the `<dataSource` which can be referenced by reports, queries and views.
* A `<schema>` which identifies the tables, views and relationships between these objects within the datamart.
* A `<flows>` element which defines one or more data flows and data pipelines for extracting data from one or SanteDB data sources (including other data marts) to populate the new data mart.

Previous versions of SanteDB (namely OpenIZ and SanteDB 1.0) shipped with a series of ETL jobs written in Talend, however this solution was not portable, and did not allow definition of data marts in an end-user conifgurable manner, and also did not work on the mobile application environment. The new SanteDB 3.0 data mart seeks to resolve this limitation.

## Defining a Datamart

Datamarts are defined by create a new asset file in the `bi/` folder of your applet. The XML file has a structure as illustrated below:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<?xml-model href="~/.ref/schema/BusinessIntelligence.xsd" 
     type="application/xml" schematypens="http://www.w3.org/2001/XMLSchema"?>
<BiDatamartDefinition xmlns="http://santedb.org/bi" 
    id="org.example.bi.datamart.example"
    name="my-datamart" label="my-datamart">

  <meta status="active" version="1.0">
    <authors>
      <add>YourCo Inc.</add>
    </authors>
    <annotation>
      <div xmlns="http://www.w3.org/1999/xhtml">
        <p>
          This is an example!
        </p>
      </div>
    </annotation>
  </meta>

  <!-- If your data-mart is a copy and extension of an existing mart -->
  <basedOn ... >
  
  <!-- If your data-mart definition adds to another data-mart that already exists -->
  <extends ...>
  
  <!-- The data source that this data mart produces -->
  <produces ... >
  
  <!-- The schema of your data mart -->
  <schema ...>
  
  <!-- The name of the data flow where the ETL process should start 
       Note: The default is a data flow named "main" -->
  <entry ...>
  
  <!-- Data Flows in the Data-Mart -->
  <dataFlows ...> 
  
</BiDatamartDefinition>
```

## Deriving / Extending Data Marts

SanteDB 3.0 provides a default datamart named `org.santedb.bi.dataSource.warehouse`, and other projects developed by SanteSuite (such as SanteEMR, SanteIMS) may have their own. Implementers can either extend these data marts or base entirely new marts on them.&#x20;

### Extending an Existing Mart

Extending an existing data mart is useful when:

* You wish to add new views to an already existing mart
* You wish to add new tables to an existing mart
* You wish to change or modify data in an existing mart after it is populated (post processing tasks)

To extend a data-mart, the `extends` element is used with a reference to the other data mart

```xml
<BiDatamartDefinition xmlns="http://santedb.org/bi" 
    id="org.example.bi.datamart.extension"
    name="extends-core" label="extends-core">
   
   <meta status="active" version="1.0">
    <authors>
      <add>YourCo Inc.</add>
    </authors>
    <annotation>
      <div xmlns="http://www.w3.org/1999/xhtml">
        <p>Adds FOO_TBL to the core data mart</p>
      </div>
    </annotation>
  </meta>
  <extends ref="#org.santedb.bi.dataSource.warehouse" />
  <schema>
    <table name="FOO_TBL">
      <column type="string" name="BAR" />
      <parent ref="ENT_TBL" />
    </table>
  </schema>
</BiDatamartDefinition>    
```

### Deriving a New Mart

It is also possible for developers to base an entirely new data mart on an existing definition. When using a derivation, the underlying mart definition is "copied", this saves developers from re-defining common assets.

Deriving a data-mart is done with the `basedOn` element.

## Produced Data Source

The primary purpose of the data mart is to provide a [BI data source](../../../extending-santesuite/extending-santedb/applets/business-intelligence-bi-assets/bi-asset-definitions/data-sources.md) which can be used for reports, queries, or like any other connection in SanteDB. The data source which is created or used as the output for the data mart is identified in the `<produces` element of the datamart definition.

### Existing Data Source

If you would like to output your data mart to an existing BI data source, use the `ref` option.

```
<produces ref="#org.santedb.bi.dataSource.main" />
```

### Configured Database

If you have configured a connection string in the SanteDB server configuration or would like to place the output of your datamart in an existing location you can specify the `connectionString` attribute on your datamart definition.

```xml
<produces id="org.example.bi.mart.example" name="example" 
     connectionString="nameOfConnectionStringInFile" />
```

### New Database

If you would like the BI layer to create a new database on your database server, you can simply specify the name, permissions, and other metadata for your new data source.

```xml
<produces id="org.example.bi.mart.example" name="example">
 <meta status="active">
   <policies>
     <!-- This requires query clinical data -->
     <demand>1.3.6.1.4.1.33349.3.1.5.9.2.2.0</demand>
   </policies>
  </meta>
</produces>
```

{% hint style="info" %}
You can specify a different databse server and technology for all data marts by creating a new connection string in your server configuration file with the `biSkel` attribute.
{% endhint %}

## Schema Definition

The `<schema>` element of the data mart definition is used to define the tables and views for the data mart in a database technology agnostic manner.

For example, to define a data mart which has two tables `FACILITY_TBL`, `PATIENT_BY_DOB_TBL`:&#x20;

```xml
<BiDatamartDefinition xmlns="http://santedb.org/bi" 
    id="org.example.bi.datamart.extension"
    name="extends-core" label="extends-core">
    
    ...
    
    <schema>
        <table name="FACILITY_TBL">
            <column type="uuid" name="ID" key="true" notNull="true" />
            <column type="string" name="NAME" />
        </table>
        
        <table name="PATIENT_BY_DOB">
            <column type="date" name="DOB" key="true" notNull="true" />
            <column type="ref" name="FACILITY_ID">
                <otherTable ref="FACILITY_TBL" />
            </column>
            <column type="integer" name="MALES" />
            <column type="integer" name="FEMALES" />
        </table>
    </schema>
    
    ...
    
</BiDatamartDefinition>
```

### Basic Table Definition

The basic table definition in a schema is expanded below:

```
<table name="{NAME_OF_TABLE}" temporary="true|false" tableSpace="{NAME_OF_TABLESPACE}">
    <column
        name="NAME_OF_COLUMN"
        type="integer|date|date-time|string|uuid|ref|decimal|bool"
        key="true|false"
        index="true|false"
        unique="true|false"
        notNull="true|false">
        <otherTable ref="{FOREIGN_KEY_TABLE}" />
    </column>
    <parent ref="{NAME_OF_PARENT_TABLE}" />
</table>
```

### Foreign Keys

Links between tables can be established using a `type="ref"` on your column and including an `<otherTable>` reference. For example, to link an `ADDRESS` table to a `PATIENTS` table:

```
<table name="PATIENTS">
    <column type="uuid" name="PATIENT_ID" key="true" />
    <column type="date" name="DATE_OF_BIRTH" />
</table>
<table name="ADDRESS">
    <column type="uuid" name="ADDRESS_ID" key="true" />
    <column type="ref" name="PATIENT_ID">
        <otherTable ref="PATIENTS" />
    </column>
    <column type="string" name="CITY" />
</table>
```

Would result in a schema where:

<figure><img src="../../../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

### Parent Tables

SanteDB's primary CDR stores data as a series of objects in a hierarchy (see:  [Conceptual Information Model](../../../../santedb/data-and-information-architecture/conceptual-data-model/)). In a relational database this is represented as "table per class" pattern, using the entity classes, this can be represented as.

<figure><img src="../../../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

This means that every `Place`, `Person`, `Patient`, and `Provider` should have an entry in `Entity` as well with the core data elements. Each other table merely adds more data to the previous.&#x20;

The BI schema definition allows the devleoper to shortcut this, and automatically create views which link these tables up the hierarchy using the `<parent>` element on the table, for example:

```xml
<table name="PERSON">
    <column name="PERSON_ID" type="uuid" key="true" />
    <column name="GENDER" type="string" index="true" />
    <column name="FIRST_NAME" type="string" />
    <column name="LAST_NAME" type="string" />
</table>
<table name="PATIENT">
    <parent ref="PERSON" />
    <column type="string" name="MRN" notNull="true" />
    <column type="ref" name="MOTHER">
        <otherTable ref="PERSON" />
    </column>
    <column type="ref" name="FATHER">
        <otherTable ref="PERSON" />
    </column>
</table>
```

Would allow a `PATIENT` to have a `MOTHER` which is either just a `PERSON` (who has only a gender, first and last name), or a `PATIENT` with an MRN.

The BI layer also automatically establishes a view `VW_PATIENT` which can be used to get all applicable fields for the `PATIENT`. The SQL generated for this definition is similar to:

```sql
CREATE TABLE PERSON (
    PERSON_ID UUID NOT NULL,
    GENDER TEXT,
    FIRST_NAME TEXT,
    LAST_NAME TEXT,
    CONSTRAINT PK_PERSON PRIMARY KEY (PERSON_ID)
)
CREATE INDEX PERSON_GENDER_IDX ON PERSON(GENDER);
CREATE TABLE PATIENT (
    MRN TEXT NOT NULL,
    MOTHER UUID,
    FATHER UUID,
    PERSON_ID UUID NOT NULL,
    CONSTRAINT PK_PATIENT PRIMARY KEY (PERSON_ID),
    CONSTRAINT FK_PATIENT_PARENT FOREIGN KEY (PERSON_ID) REFERENCES
        PERSON(PERSON_ID),
    CONSTRAINT FK_PATIENT_MOTHER FOREIGN KEY (PERSON_ID) REFERENCES
        PERSON(PERSON_ID),
    CONSTRAINT FK_PATIENT_FATHER FOREIGN KEY (PERSON_ID) REFERENCES
        PERSON(PERSON_ID)
);
CREATE VIEW VW_PATIENT AS
    SELECT MRN, MOTHER, FATHER, PERSON_ID, GENDER, FIRST_NAME, LAST_NAME
    FROM PATIENT
        INNER JOIN PERSON USING(PERSON_ID);
```

## Data Flows

The schema of the data mart defines its structure, the data flows of the data mart definition describe how data is extracted from another source to populate the data mart.

```xml
<dataFlows>
    <flow name="{DATA_FLOW_NAME}">
        <parameters>
            <int|string|ref|bool|uuid name="{NAME_OF_PARAMETER}" />
            <int|string|ref|bool|uuid name="{NAME_OF_PARAMETER}" />
        </parameters>
        <pipeline>
            <!-- Pipeline Steps here -->
        </pipeline>
        <return ref="{REFERENCE_TO_PIPELINE_OUTPUT_TO_RETURN}" />
    </flow>
    <flow name=....
</dataFlows>
```

Each data flow defines one or more parameters (which can be passed by a caller) and a single data pipeline.&#x20;

### Data Pipeline

The order of the elements in the `<pipeline>` element don't necessarily have an impact on the order in which the items are called, the execution of a data pipeline starts with all un-streamed components and works backwards. This creates a streaming `IEnumerable` data flow for each component, for example:

```xml
<flow name="example">
    <pipeline>
        <connection name="inputConnection" mode="read-only">
            <dataSource ref="#org.santedb.bi.dataSource.main" />
        </connection>
        <connection name="outputConnection" mode="read-write">
            <dataSource ref="#org.example.bi.mart.example" />
        </connection>
        <reader name="read_addresses">
            <connection ref="inputConnection" />
            <sql>
                <add>
                    <![CDATA[  
                        SELECT ENT_ID, MNEMONIC, VAL
                        FROM ENT_ADDR_CMP_TBL
                           INNER JOIN CD_VRSN_TBL ON (TYP_CD_ID = CD_ID)
                    ]]>
                </add>
            </sql>
        </reader>
        <crosstab name="pivot_addresses">
            <input ref="read_addresses" />
            <pivot fn="first" key="ent_id" value="val" columnDef="mnemonic">
                <columns>
                    <add>Country</add>
                    <add>City</add>
                    <add>AddressLine</add>
                    <add>PostalCode</add>
                </columns>
            </pivot>
        </crosstab>
        <writer mode="insert" truncate="true" name="write_address">
            <input ref="pivot_addresses" />
            <connection ref="outputConnection" />
            <target ref="ADDRESSES" />
        </writer>
    </pipeline>
    <return ref="write_addresses" />
</flow>
```

The execution engine analysis would conclude that the terminal node of this pipeline is the `<writer>` step, which relies on `<crosstab>` which relies on `<reader>` so the order of  execution would be:

* Open connection `inputConnection`
* Execute SQL and name the stream `read_addresses`
* Pivot the output of `read_addresses` and namd the stream `pivot_addresses`
* Open the `outputConnection` connection
* Write the stream `pivot_addresses` to the `outputConnection`

### Pipeline Steps

The `<pipeline>` element of a flow represents the activities which are to be performed for the flow. Each pipeline step must carry a `name=""` attribute, and should reference other steps where possible. For example, referencing components is performed with the `ref=""` attribute as illustrated below:

```
<connection name="myConnection">
    ...
</connection>
<reader name="myReader">
    <connection ref="myConnection" />
    ...
</reader>
<writer name="myWriter">
    <input ref="myReader" />
    <connection ref="myConnection" />
    target ref="myTable" />
</writer>
```

#### Connect to Database

**Input:** None\
**Output:** `DataIntegrationConnection`

Connections to the database are made using the `<connection>` pipeline step. The connection pipeline step is illustrated below.

```xml
<connection name="{NAME_OF_CONNECTION}" mode="read-write|read-only">
    <dataSource ref="{REFERENCE_TO_OTHER_DATASOURCE} connection="connectionStringName" />
</connection>
```

| Property                 | Values                      | Description                                                                                                                                       |
| ------------------------ | --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| `@name`                  | String                      | Identifies the name of the connection for referencing in other data components.                                                                   |
| `@mode`                  | `read-only` or `read-write` | Indicates the connection mode. Using `read-only` for source data is recommended as it allows the data source to connect a replica (if configured) |
| `dataSource/@ref`        | Reference                   | If the connection is using an already defined BI data source, this is the reference to that data source.                                          |
| `dataSource/@connection` | Connection String           | The connection string in the SanteDB configuration to the database (for direct connections)                                                       |

For example, to define a connection to the main SanteDB iCDR database:

```xml
<connection name="mainDatabase" mode="read-only">
   <dataSource ref="#org.santedb.bi.dataSource.main" />
</connection>
```

#### Execute in Transaction

**Input:** `DataIntegrationConnection`\
**Output**: `DataStream`

When executing multiple operations, it is often desirable to execute the output in a transaction. Transactions represent an atomic series of updates, and either all the components succeed, or none do. Transactions create a new sub-scope from the data flow which contains them.

```xml
<transaction name="{NAME_OF_TRANSACTION}">
    <connection ref="{NAME_OF_CONNECTION}" />
    <pipeline>
        <!-- Pipeline Here -->
    </pipeline>
</transaction>
```

The transaction requires that the connection be opened in `read-write` mode.

| Property     | Values                                               | Description                                                                      |
| ------------ | ---------------------------------------------------- | -------------------------------------------------------------------------------- |
| `@name`      | String                                               | Identifies the name of the transaction for referencing in other data components. |
| `connection` | Reference to connection step or an inline connection | The connection object which the transaction should be executed on.               |
| `pipeline`   | List of Steps                                        | The pipeline steps to execute in the transaction                                 |

For example:

```xml
<connection name="outputConnection" mode="read-write">
   <dataSource ref="#org.santedb.bi.dataSource.warehouse" />
</connection>
<connection name="inputConnection" mode="read-only">
  <dataSource ref="#org.santedb.bi.dataSource.main" />
</connection>
<reader name="read_addresses">
   <connection ref="inputConnection" />
   <sql>
       <add>
          <![CDATA[  
              SELECT ENT_ID, MNEMONIC, VAL
              FROM ENT_ADDR_CMP_TBL
               INNER JOIN CD_VRSN_TBL ON (TYP_CD_ID = CD_ID)
            ]]>
        </add>
    </sql>
</reader>
<transaction name="main_transaction">
    <connection ref="warehouseDatabase" />
    <writer name="write_addresses">
        <intput ref="read_addresses" />
        <connection ref="outputConnection" />
        <target="ADDRESS_TABLE" />
    </writer>
    <filter name="reject_filter">
        <input ref="write_addresses" />
        <when column="$reject" op="eq" value="true" />
    </filter>
    <writer name="write_rejects">
        <input name="reject_filter" />
        <connection ref="outputConnection" />
        <target ref="ADDRESS_REJECTS" />
    </writer>
</transaction>        
```

#### Call Flow

**Input:** None\
**Output:** `DataStream`

The `<call>` pipeline instruction can be used to call another flow and pass parameter arguments to the called flow.

```
<call name="{NAME_OF_CALL}">
    <dataFlow ref="{OTHER_FLOW_TO_CALL}" />
    <args>
        <int|string|bool|uuid|date|date-time|ref name="NAME_OF_PARAMETER">
            <value />
        </int|string|bool|uuid|date|date-time|ref>
    </args>
</call>
```



| Property        | Value                                  | Description                                                       |
| --------------- | -------------------------------------- | ----------------------------------------------------------------- |
| `dataFlow/@ref` | Reference to DataFlow                  | The data flow which is to be executed/called.                     |
| `args/*`        | The argument list indicating the type  | One or more arguments which are identiifed by their argument type |
| `args/*/@name`  | String                                 | Name of the argument being passed                                 |
| `args/*/value`  | Variable                               | The value to pass as the variable                                 |

For example, to call `FOO_FLOW` passing the input connection and a flag, and then output the result to the log:

```xml
<call name="call_foo">
    <dataFlow ref="FOO_FLOW" />
    <args>
        <ref name="connection">
            <value ref="inputConnection" />
        </ref>
        <bool name="ignoreOld">
            <value>true</value>
        </bool>
    </args>
</call>
<log name="log_foo">
    <input ref="call_foo" />
</log>
```

#### Data Reader

**Input:** `DataIntegrationConnection`\
**Output:** `DataStream`

A data reader is used to open a streaming result set based on a SQL query executed against a connection.

```
<reader name="{NAME_OF_RESULTING_READER_STREAM}">
    <connection ref="{CONNECTION_TO_READ_FROM}" />
    <sql>
        <add>
            <providers>
                <invariant>sqlite|FireirdSQL|npgsql</invariant>
            </providers>
            <![CDATA[ SQL TO EXECUTE ]]>
        </add>
    </sql>
    <schema ref="{REFERENCE_TO_TABLE}">
        <columns ... />
    </schema>
</reader>
```

| Property            | Value           | Description                                                                                             |
| ------------------- | --------------- | ------------------------------------------------------------------------------------------------------- |
| `@name`             | Name            | The name of the stream output that the reader creates (to be used in subsequent flow steps with `@ref`) |
| `connection/@ref`   | Data Source     | The data source or data connection step that should be used to execute the SQL                          |
| `sql/add`           | SQL             | The SQL statement to be added for the dialects of SQL indicates in `providers`                          |
| `sql/add/providers` | Provider Name   | The SQL providers that the SQL applies to.                                                              |
| `schema/@ref`       | Table Reference | A reference to the table which contains the schema the output is expected to be in.                     |
| `schema/columns`    | Table           | If defining a schema inline, the columns returned by the SQL.                                           |

For example, to read all identiifers in the SanteDB primary database.

```xml
<reader name="source_ent_id">
  <connection ref="input" />
  <schema>
      <column name="ENT_ID_ID" type="uuid"/>
      <column name="ENT_ID" type="uuid"/>
      <column name="VALUE" type="string"/>
      <column name="ISSUER" type="string"/>
      <column name="CHECK_DIGIT" type="string"/>
      <column name="ISSUED" type="date"/>
      <column name="EXPIRY" type="date"/>
  </schema>
  <sql>
    <add>
      <providers>
        <invariant>npgsql</invariant>
        <invariant>FirebirdSQL</invariant>
        <invariant>sqlite</invariant>
      </providers>
      <![CDATA[ 
                SELECT 
                    ENT_ID_TBL.ENT_ID_ID,
                    ENT_ID_TBL.ENT_ID,
                    ID_VAL AS VALUE,
                    ID_DMN_TBL.NSID AS ISSUER,
                    CHK_DGT AS CHECK_DIGIT,
                    ISS_DT AS ISSUED,
                    EXP_DT AS EXPIRY
                FROM
                    ENT_ID_TBL
                    INNER JOIN ID_DMN_TBL USING (DMN_ID)
                WHERE
                    ENT_ID_TBL.OBSLT_VRSN_SEQ_ID IS NULL
                    AND ID_DMN_TBL.OBSLT_UTC IS NULL
                ]]>
    </add>
  </sql>
 </reader>
```

#### Data Writer

**Input:** `DataStream`\
**Output:** `DataStream`

#### Column Mapping

**Input:** `DataStream`\
**Output:** `DataStream`

#### Crosstab

**Input:** `DataStream`\
**Output:** `DataStream`

#### Output to Log

**Input:** `DataStream`\
**Output:** `DataStream`
