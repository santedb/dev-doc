# External Data Maps

SanteDB 3.0 allows for developers to specify external data maps which can be used in their project to import data that is alien to SanteDB. These definition files are located in the `alien/` directory of your applet.

{% hint style="info" %}
In Visual Studio Code, you can use an XML editing plugin and bind the ForeignDataMap.xsd schema to your file to obtain auto-complete information via the \`

```xml
<?xml-model href="../.ref/schema/ForeignDataMap.xsd" 
   type="application/xml" 
   schematypens="http://www.w3.org/2001/XMLSchema"?>
```
{% endhint %}

## General Structure

A single data map definition may contain multiple `<map>` elements. These maps generate a transaction bundle which is translated and imported. The overall structure of a map file is illustrated below.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<?xml-model href="../.ref/schema/ForeignDataMap.xsd" type="application/xml" 
     schematypens="http://www.w3.org/2001/XMLSchema"?>
<ForeignDataMap xmlns="http://santedb.org/import">
    <id>00000000-0000-0000-0000-000000000000</id>
    <name>My Foreign Data Mapping</name>
    <description>This does some things with a file</description>
    <creationTime />
    <maps>
        <map>
            <resource type="Type1"/>
                <when>
                    <source />
                    <value />
                </when>
                <maps>
                    <map required="true|false" replace="true|false" whenTargetMissing="Error|Warning|Information">
                        <source>Field_Name</source>
                        <when>
                           <value/>
                        </when>
                        <fixed when="?">Value to fix</fixed>
                        <transform transformer="name">
                            <args />
                        </transform>
                        <target>targetHDSIPath</target>
                    </map>
                </maps>
                <existing>
                    <where>id=$output.id</where>
                </existing>
            </resource>
            <resource type="Type2" />
        </map>
    </maps>
</ForeignDataMap>
```

## Resource Maps

A single `<map>` element can contain one or more resources. Each `<map>` is translated into a transaction bundle, meaning that if any of the translated resources have an issue with persistence then none of the resources are committed.

The resource map has three instructions:

* `when` - Which is evaluated against the input data to determine whether the resource map applies to the data (for example - if creating a Place to support a birthplace)
* `maps` - Which are a series of mappings which translate the input data to an output structure.
* `existing` - Which is used to query the database to determine whether the data already exists in the database.

For example, consider an input source in CSV such as:

```
id,fname,gname,age,mother,father,town,province,birth_facility_type,birth_facility
"A1023","SMITH","BOB",34,"SALLY SMITH","ROGER SMITH","Sometown","Ontario","HOSPITAL", "Good Hospital"
```

### Conditional Resource Mapping

The `<when>` is used to control whether the mapping instructions are applied to the input data. The when structure is evaluated against an input field with one or more values. For example to create a Place when the value in `birth_facility_type` is HOSPITAL or CLINIC:

```xml
<resource type="Place">
    <when>
        <source>birth_facility_type</source>
        <value>HOSPITAL</value>
        <value>CLINIC</value>
    </when>
```

### Field Mapping

Fields are mapped against a source, a fixed value, or a programmatic transform.&#x20;

#### Simple Mapping

The simplest mapping is when a value in a source field is directly copied to a target. The target is expressed as an HDSI path. For example, to map the `fname` field in the input to the given name:

```
<resource type="Patient">
    ...
    <maps>
       <map required="true" replace="true">
           <source>fname</source>
           <target>name[OfficialRecord].component[Given].value</target>
       </map>
       ...
```

#### Fixed Value

A map can also be sourced from a fixed value - this is useful when you want to set a fixed value to a field such as a typeCode, or an address part. For example, to fix the country of the patient's address to CA:

```
<resource type="Patient">
    ...
    <maps>
       <map>
          <fixed>CA</fixed>
          <target>address[HomeAddress].component[Country].value</target>
       </map>
```

Fixed values can also be assigned based on a when condition. For example, to select a different class code based on a number in a source column:

```
<maps>
    <map>
        <source>birth_facility_type</source>
        <fixed when="HOSPITAL">fc....</fixed>
        <fixed when"CLINIC">ea.....</fixed>
        <target>typeComcept</target>
    </map>
```

#### Transforming Values

Values can be transformed from their source into other forms using one of the built-in transformers avaialble. Transformed values are applied against their input value, for example - to look-up the birthplace based on the facility name only when the type of a HOSPITAL or CLINIC:

```
<map>
   <source>birth_facility</source>
   <when>
      <source>birth_facility_type</source>
      <value>HOSPITAL</value>
      <value>CLINIC</value>
   </when>
   <transform transformer="EntityLookup">
      <args>
         <string>Place</string>
         <string>classConcept=ff34dfa7-c6d3-4f8b-bc9f-14bcdc13ba6c&amp;name.component.value=$input</string>
      </args>
   </transform>
   <target>relationship[Birthplace].target</target>
</map>
```

The transformers available are:

| Transformer         | Arguments                                                   | Description                                                                                                                                                                                                                                      |
| ------------------- | ----------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| EntityLookup        | <p>Entity Type<br>Lookup Expression<br>Value Expression</p> | Queries the persistence layer for the first argument type using the lookup expression procided. Field values can be accessed as HDSI variables such as `$fname` or `$gname` , or the `$input` variable can be used for the current input column. |
| CamelCase           |                                                             | Converts the current `$input` to CamelCase. For example `nurse practitioner specialist` will be transformed to `NursePractitionerSpecialist`                                                                                                     |
| AgeCalculation      |                                                             | Calculates a date time based on a number which represents the age of the object at a particular time.                                                                                                                                            |
| Expression          | Expression String                                           | Executes a C# expression where each input field is a `$variable` . This can be used to perform mathematical operations.                                                                                                                          |
| NoCase              | Case Selection                                              | Converts the input  lower case when the argument is `l` or upper case when the argument is `u`                                                                                                                                                   |
| Prefix              | Prefix Text                                                 | Prepends the input value with the argument supplied.                                                                                                                                                                                             |
| ReferenceTermLookup | Code System                                                 | Performs a reference term lookup against the input value in a standardized code system.                                                                                                                                                          |
| EpochToDate         | Truncation Method                                           | When a column is represented in as a unix epoch - this will convert the value to a proper date and time.                                                                                                                                         |

