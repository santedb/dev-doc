# BRE Debugger

## SanteDB Debugger Reference

The SanteDB debugger is a tool that allows developers to interactively debug business rules, and clinical protocols before pushing these changes to a production or staging environment.

### Command Line Options

**Tool:** sdb-dbg.exe

The following parameters are supported by the SanteDB debugger

| Option | Description | Example |
| :--- | :--- | :--- |
| source | Source code file\(s\) for debugging | --source=myrule.js |
| workDir | Working directory for the debugger | --workDir=C:\users\myuser\sources |
| db | Attached sqlite database for loading / inserting data operations | --db=%localppdata%\sdbare\santedb.sqlite |
| config | Attached configuration file for debugging | --config=C:\temp\santedb.config |
| ref | Loads rules and script files from the referenced PAK file | --ref=org.santedb.core.sln.pak |
| bre | Launches the debugger in BusinessRules mode \(debug JavaScript rules\) | --bre |
| xprot | Launches the debugger in ClinicalProtocol mode \(debug XProtocol files\) | --xprot |

### Debug Shell

The debug shell provides basic common commands as well as debugger specific commands \(for JavaScript or XProtocol\).

### Common Commands

| Command | Name |
| :--- | :--- |
| cd | Change Directory |
| sn | Scope to Null |
| clear | Clear Screen |
| ds | Dump Scope |
| dj | Dump Scope JSON |
| dv | Dump Scope View Model |
| dx | Dump Scope XML |
| xs | Exchange Scope |
| q | Quit |
| ? | Show Help |
| dbi | Database Insert |
| lds | List Data Services |
| ls | List Directory |
| ofs | Output Full Stack |
| pdq | Print Data Query |
| pwd | Print Working Directory |
| ss | Set Scope |
| sd | Set Scope - Database Object |
| sdq | Set Scope - Database Query |
| sfv | Set Scope - View Model File |
| sfj | Set Scope - JSON File |
| sfx | Set Scope - XML File |

#### cd - Change Directory

Changes the working directory **Example:** cd C:\sources

#### sn - Scope to null

Sets the current scope to NULL

#### clear - Clear Screen

Clears the current screen

#### ds - Dump Scope

Dumps the current scope to the screen in .NET format

**Parameters**

* \[path\] - The object property path to be dumped

**Example: Dump Scope**

```text
dbg >ds
Type: SanteDB.Core.Model.Roles.Patient
Asm:  SanteDB.Core.Model, Version=1.0.0.22772, Culture=neutral, PublicKeyToken=null
Str:  Patient (K:, V:)
Addresses                 List`1                    System.Collections.Generic.List`1[OpenIZ.Core.Model.Entities.EntityAddress]
AsSecurityUser            SecurityUser              null
ClassConcept              Concept                   null
ClassConceptKey           Nullable`1                bacd9c6f-3fa9-481e-9636-37457962804d
```

**Example: Dump Scope with Path**

```text
dbg >ds DateOfBirth
Type: SanteDB.Core.Model.Roles.Patient
Asm:  SanteDB.Core.Model, Version=1.0.0.22772, Culture=neutral, PublicKeyToken=null
Str:  Patient (K:, V:)
Path: DateOfBirth
5/22/1986 12:00:00 AM
```

#### dj - Dump JSON

Dumps the current scope object to HDSI JSON format

**Parameters**

* \[path\] - The object property path to be dumped

**Example: Dump Scope as JSON**

```text
dbg >dj
{
  "dateOfBirth": "1986-05-22",
  "language": [],
  "classConcept": "bacd9c6f-3fa9-481e-9636-37457962804d",
  "determinerConcept": "f29f08de-78a7-4a5e-aeaf-7b545ba19a09",
  "relationship": [],
  "$type": "Patient"
}
```

#### dv - Dump View Model

Dumps the current scope object as ViewModel format

**Remarks**: This command is useful when debugging data which is being sent to the view model in the AngularJS controllers

**Example: Dump Scope as ViewModel**

```text
dbg >dv
{
  "$type": "Patient",
  "$id": "obj0",
  "dateOfBirth": "1986-05-22",
  "address": {},
  "identifier": {},
  "name": {},
  "relationship": {},
  "telecom": {},
  "creationTimeModel": "0001-01-01T00:00:00+00:00"
}
```

#### dx - Dump XML

Dumps the current scope object as IMSI XML format

**Parameters:**

* \[path\] - The path within the object which should be dumped to screen

**Example: Dump Scope as XML**

```text
dbg >dx
<Patient xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://santedb.org/model">
  <version xsi:nil="true" />
  <sequence xsi:nil="true" />
  <classConcept>bacd9c6f-3fa9-481e-9636-37457962804d</classConcept>
  <determinerConcept>f29f08de-78a7-4a5e-aeaf-7b545ba19a09</determinerConcept>
  <statusConcept xsi:nil="true" />
  <dateOfBirth>1986-05-22</dateOfBirth>
  <genderConcept xsi:nil="true" />
</Patient>
```

#### xs - Exchange Scope

Exchanges the scope for a child element of the current scope.

**Parameters:**

* \[path\] - The path within the current scope object to exchange the debugging scope with

**Example: Exchange Scope for Array Item** Sets scope to a query then exchanges scope to first search result:

```text
dbg >ds
Type: System.Collections.Generic.List`1[[SanteDB.Core.Model.Roles.Patient, OpenIZ.Core.Model, Version=1.0.0.22772, Culture=neutral, PublicKeyToken=null]]
Asm:  mscorlib, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089
Str:  System.Collections.Generic.List`1[SanteDB.Core.Model.Roles.Patient]
Count:10
[0] Patient (K:16f27afe-4966-4c85-956c-90dfaba62446, V:bf3deb9e-29e9-4146-8ada-4ba7871d12e6)
[1] Patient (K:55080b7a-3da6-4992-96bb-a6d20bf17b13, V:be2396ec-1786-46f3-8beb-8f203bae3941)
[2] Patient (K:e45fcadf-e3af-43e7-953e-4a8125f2d6a0, V:0fc264e5-addd-4103-9c40-d23f2d9f703b)
[3] Patient (K:df5dde4a-a33b-4abe-95fd-63d58e1b96f0, V:6b10fb8c-295f-4f6e-b11b-48e40198c935)
[4] Patient (K:be6420ac-6ba8-4faa-98f6-7d9efdcd04a0, V:1c0749f3-bcdf-42af-a36a-03f702adc336)
[5] Patient (K:7f649985-0d97-4d04-a6a1-502c67c35327, V:ed255f0a-8617-4639-a4af-de3e272bb862)
[6] Patient (K:8289fa5e-7c08-4075-9a91-8e79bebaca3f, V:88965abd-32b8-4b29-8d4d-060417c6187e)
[7] Patient (K:cd1c6592-fec0-4a7b-ab0a-4ca51fce801c, V:c8d267cf-9845-4a8c-a6fd-1563ab204971)
[8] Patient (K:10abe6c3-22d5-4804-9090-164098a1eb65, V:27a04a6c-96ef-4b95-aac3-d43efa810485)
[9] Patient (K:f82e9145-2aa0-416a-bbda-41656b7e8eff, V:5044a736-5c07-439c-8f17-5d04d3460dac)
dbg >xs [0]
Path: [0]
dbg >ds
Type: SanteDB.Core.Model.Roles.Patient
Asm:  SanteDB.Core.Model, Version=1.0.0.22772, Culture=neutral, PublicKeyToken=null
```

#### q - Quit

Exits the debugger

#### ? - Show Help

Shows a complete list of commands for the current debugger

#### dbi - Database Insert

Inserts the current scope object into the database, setting the scope variable to the inserted instance.

#### lds - List Data Services

Lists all loaded services in the debugger environment

#### ls - List Directory

Lists the current working directory contents

**Parameters:**

* \[dir\] - The subdirectory to list contents of

#### ofs - Output Full Stack

Output full stack traces instead of the summarized stack traces.

#### pdq - Print Data Query

Executes a database query against the attached database, however does not set the scope.

**Remarks:** This is useful when you want to query the database but do not want to set the scope \(i.e. finding a record you will later set the scope to\) **Parameters**

* \[type\] - The type of resource being queried
* \[qry\] - The HDSI format query to be executed
* \[skip\] - Skips the number of records
* \[take\] - Takes the specified number of records from the dataset
* \[path\] - The sub-path within the query result to show

**Valid Uses:**

*  `pdq [type] [qry]` - Simple query
*  `pdq [type] [qry] [path]` - Simple query, printing path
*  `pdq [type] [qry] [skip] [take]` - Query with result control limits
*  `pdq [type] [qry] [skip] [take] [path]` - Query with control limits, output selected path

**Example: Query for patients with name Justin and show the first result's address**

```text
dbg >pdq Patient name.component.value=Justin [0].Addresses
INF: Patient where o => o.Names.Any(name => name.Component.Any(component => (component.Value == "Justin"))) (0..)
Path: [0].Addresses
Count:1
[0] SanteDB.Core.Model.Entities.EntityAddress
```

#### pwd - Print Working Directory

Prints the current working directory to the screen.

#### ss - Set Scope

Sets the scope to the specified simple object

**Parameters:**

* \[scope\] - The simple object to set to scope
* \[type\] - The type of resource to set scope to
* \[data\] - The JSON formatted data to set the typed scope to \(can only be used with type\)

**Valid Uses:**

*  `ss [scope]` - Simple Data
*  `ss [type] [data]` - Complex data from JSON

**Example: Set scope to 'hello world!'**

```text
dbg >ss 'Hello World!'
dbg >ds
Type: System.String
Asm:  mscorlib, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089
Str:  Hello World!
Hello World!
```

**Example: Set scope to a patient with date of birth of March 1, 2017**

```text
dbg >ss Patient '{"dateOfBirth":"2018-03-17"}'
dbg >ds
Type: SanteDB.Core.Model.Roles.Patient
Asm:  SanteDB.Core.Model, Version=1.0.0.22772, Culture=neutral, PublicKeyToken=null
Str:  Patient (K:, V:)
Addresses                 List`1                    System.Collections.Generic.List`1[OpenIZ.Core.Model.Entities.EntityAddress]
AsSecurityUser            SecurityUser              null
ClassConcept              Concept                   null
ClassConceptKey           Nullable`1                bacd9c6f-3fa9-481e-9636-37457962804d
CreatedBy                 SecurityUser              null
CreatedByKey              Nullable`1                null
CreationAct               Act                       null
CreationActKey            Nullable`1                null
CreationTime              DateTimeOffset            1/1/0001 12:00:00 AM +00:00
CreationTimeXml           String                    null
DateOfBirth               Nullable`1                3/17/2018 12:00:00 AM
```

#### sd - Set Database Scope

Sets the current scope from the specified database object.

**Remarks:** This command is useful when reproducing bugs with a known patient identifier.

**Parameters:**

* \[type\] - The resource type of data to load
* \[id\] - The identifier of the data to be loaded

**Example: Load patient with ID be6420ac-6ba8-4faa-98f6-7d9efdcd04a0 to scope**

```text
dbg >sd Patient be6420ac-6ba8-4faa-98f6-7d9efdcd04a0
dbg >ds
Type: SanteDB.Core.Model.Roles.Patient
Asm:  SanteDB.Core.Model, Version=1.0.0.22772, Culture=neutral, PublicKeyToken=null
Str:  Patient (K:be6420ac-6ba8-4faa-98f6-7d9efdcd04a0, V:1c0749f3-bcdf-42af-a36a-03f702adc336)
...
```

#### sdq - Set Database Scope Query

Sets the current scope to the result of a query with optional controls

**Remarks:** This operation is useful when you don't know the key of the data in a database to reproduce an issue, however you know attributes of the data.

**Parameters:**

* \[type\] - The type of data to be queried
* \[qry\] - The query to be executed
* \[skip\] - The number of results to skip in the result set
* \[take\] - The number of results to take

**Valid Uses:**

*  `sdq [type] [qry]` - Set scope to results of query
*  `sdq [type] [qry] [skip] [take]` - Set scope to results of query with result control

**Example: Set scope to all Patients having an external identifier of 1234567890**

```text
dbg >sdq Patient identifier.value=1234567890
INF: Patient where o => o.Identifiers.Any(identifier => (identifier.Value == "1234567890")) (0..)
INF: 1 set to scope
```

**Example: Set scope to first 10 patients with name containing 'a'**\*

```text
dbg >sdq Patient name.component.value=~*a* 0 10
INF: Patient where o => o.Names.Any(name => name.Component.Any(component => (component.Value.Contains("*a*") == True))) (0..10)
INF: 15 result (0..10 set to scope)
```

#### sfv - Set File \(View Model\)

Sets the current scope to the contents of a JSON file formatted in ViewModel format

**Parameters:**

* \[type\] - The type of data the JSON View Model file contains
* \[file\] - The name of the file to load

#### sfj - Set File JSON

Sets the current scope to the contents of a IMSI JSON file.

**Remarks:** The JSON file must carry a valid "$type" property.

**Parameters:**

* \[file\] - The file to be loaded

#### sfx - Set File XML

Sets the current scope to the contents of an IMSI XML file

**Parameters:**

* \[type\] - The type of resource the file contains
* \[file\] - The path to the XML file to load

