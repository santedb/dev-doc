# Business Rules

## &#x20;Introduction

This tutorial is intended to assist developers with the writing of business rules using the SanteDB Jint business rules engine (the default business rules engine in SanteDB).

{% hint style="info" %}
SanteDB can run rules in the user interface on demand (which run in the user's browser) otherwise they are run in the dCDR and iCDR using a C# to JavaScript interpreter bridge named [JINT](https://github.com/sebastienros/jint). The JINT library.&#x20;

* SanteDB < 2.0.x use JINT 2.0 which is compatible with ECMA Script 5.1
* SanteDB > 2.1.x use JINT 3.0 Beta which is compatible with a subset of ECMA Script 6  functions (see: [https://github.com/sebastienros/jint/blob/main/README.md](https://github.com/sebastienros/jint/blob/main/README.md))
{% endhint %}

### &#x20;What is a Business Rule?

SanteDB provides a series of extension points where developers can write custom triggers to modify, extend, add, or remove data from resources. These changes are used to implement business rules on the series of objects the subscribe to. Some examples might be:

* Interpreting an observation based on some pre-defined lookup tables
* Merging patients before they are persisted based on specified criteria
* Validating that a substance administration is correct before persisting it

{% hint style="info" %}
This article covers writing business rules in JavaScript in your applets. While this method is convenient, if you require higher performing business rules, consider implementing a [business-rules-service.md](../../../server-plugins/service-definitions/business-rules-service.md "mention")in C# instead.
{% endhint %}

### &#x20;How does SanteDB treat Business Rules?

Business rules subscribe to persistence events on the repository layer of the architecture. Whenever a piece of data is modified, these events fire, and the correlated business rules are triggered.

### &#x20;Technically how is this done?

From a technical standpoint, SanteDB (and the disconnected client) compile JavaScript into .NET code at runtime. An entire BRE script is executed on application startup (or server startup) and here the script is free to subscribe to a series of events.

These events are:

| Event          | Description                                                      |
| -------------- | ---------------------------------------------------------------- |
| BeforeInsert   | Fired before data is persisted to the database                   |
| AfterInsert    | Fired after data has successfully been persisted to the database |
| BeforeUpdate   | Fired before data is updated in the database                     |
| AfterUpdate    | Fired after data has successfully been updated in the database   |
| BeforeObsolete | Fired prior to data being obsoleted in the database              |
| AfterObsolete  | Fired after data has been obsoleted in the database              |
| BeforeQuery    | Fired before a query is run allowing the rule to change query    |
| AfterQuery     | Fired after a query has been executed and results are ready      |

Business rules which are executed before persistence (BeforeInsert, BeforeObsolete, BeforeUpdate) have the opportunity to change data that is about to be persisted. This is done by returning data from the function which is to be updated.

Business rules which are executed after persistence (AfterInsert, AfterObsolete, AfterUpdate) may also change data, however it is important to note that these are done as a separate transaction as the rules are executed after the operation has been committed to the database. This means that any operation where the "After" trigger fails, will result in a 422 response to the client, whilst the data is persisted to the database.

If your trigger requires operation within the master transaction, however you want to ensure the persistence is completed, you can return a Bundle (for a transaction) and push additional operations to the scoped bundle.

### &#x20;A simple business rule

Business rules are loaded from the rules/ folder of your applet. This tutorial will create a rule which will add a tag to a patient called "ReviewState" and will set it to "NotReviewed". This operation will illustrate the BeforeInsert rule and AfterUpdate rules.

1. Create an empty JavaScript file in the rules/ folder of your applet
2.  We need to call the SanteDBBre.AddBusinessRule() function to register our rule, we're subscribing to "Patient"s.

    ```javascript
    SanteDBBre.AddBusinessRule("id", "Patient", "BeforeInsert", [], function(patient) {

    });
    ```

    &#x20;The AddBusinessRule function accepts a callback which is to be called whenever the trigger "BeforeInsert" on a Patient is called. The \[ ] is reserved for filter properties which prevent the filter from being called.
3.  Next, we want to add a tag to this patient object, this is done using the standard SanteDB JavaScript bridge functionality you write your regular applet controller code in:

    ```javascript
    SanteDBBre.AddBusinessRule("my_patient_rule", "Patient", "BeforeInsert", [], function(patient) {

        patient.tag = patient.tag || {};
        // ensure the rule has not been run
        if(patient.tag["ReviewState"] === undefined)
            patient.tag["ReviewState"] = 'NotReviewed';
        return patient;

    });
    ```
4.  Next, we may want to add a rule for AfterUpdate which clears this tag or sets the status to reviewed (note: since AfterUpdate is called after the data is committed, we have to manually save. We could call SanteDB.resources.patient.saveAsync() however that would result in a new version. For tagging we can use the built-in SaveTags function)

    ```javascript
     SanteDBBre.AddBusinessRule("my_patient_rule", "Patient", "AfterUpdate", [], function(patient) {

         patient.tag = patient.tag || {};

         // is the state 'NotReviewed'?
         if(patient.tag["ReviewState"] == 'NotReviewed') {
             patient.tag["ReviewState"] = 'Reviewed';
             SanteDBBre.SaveTags(patient); // we updated the tag after a commit so we have to save them manully
         }

         return patient;
     });
    ```

#### &#x20;Adding Validation

Another operation that can be injected into the SanteDB logic is resource validation. If you have custom rules that you would like evaluated before a resource is saved, you can add a validation function.

For example, if we want to prevent patients from being saved without a date of birth or gender, we could write a simple validator:

```javascript
SanteDBBre.AddValidator("my_patient_validator", "Patient", function(patient) {
    var issues = [];

    if(!patient.dateOfBirth)
        issues.push({ text: 'Patients must have date of birth', priority: 1 });
    if(!patient.genderConcept)
        issues.push({ text: 'Patients must have a gender', priority: 1 });
    
    return issues;
});
```

The result of the validator function is an array of SanteDBBre.DetectedIssue instances.

### &#x20;Debugging your business rules

The SanteDB SDK provides a mechanism to debug your business rules including setting break points, stepping in/over functions, etc. These tools are provided via the `sdb-dbg` program in the SDK.

When running the SDK you must specify a disconnected client database to test with. This can acquired using several techniques:

* Creating a backup from the SanteDB Disconnected Client mobile application
* Pointing the database at a configured sdb-ade database (`--db=%localappdata%\sdbare\santedb.sqlite`). Note this is the default operating mode when launching the application from the start menu.
* Creating a new database and using anonymous patients (only recommended for simple protocols)

To debug a clinical protocol, you can use the following command:

```
> sdb-ade --db=newdb1.sqlite --bre
SanteDB Debugger v1.10.0.20334 (Fredericton)
Copyright (C) 2015-2019 Mohawk College of Applied Arts and Technology
Loading debuggees...
Working Directory: C:\Users\justin\Documents
Ready...
dbg >
```

Note that you can pre-load a script file by specifying --source= , however this tutorial, will load the file from the debug command prompt.

```
dbg >cd c:\users\justin\source\repos\applet-starter\rules
INF: c:\users\justin\source\repos\applet-starter\rules
dbg >x tageme.js
tagme.js (run) >
Execution Finished
tagme.js (idle) >
```

The command to "open" a file (`o`) will only load the file into the current source buffer, whereas "execute file" (`x`) will load the file and execute it.

We can print the file contents using the print file (`pf`) command:

```
tagme.js (idle) >pf
[1]   SanteDBBre.AddBusinessRule("Patient", "BeforeInsert", [], function(patient) {
[2]
[3]       patient.tag = patient.tag || {};
[4]       // ensure the rule has not been run
[5]       if(patient.tag["ReviewState"] === undefined)
[6]           patient.tag["ReviewState"] = 'NotReviewed';
[7]       return patient;
[8]
[9]   });

```

Setting a breakpoint is done using the break (`b`) command and a line number. For example, the commands `b 3` and then `pf 0 10` will set a breakpoint at line 3 and then print the file from lines 0 to 10:

```
tagme.js (idle) >b 3
tagme.js (idle) >pf 0 10
[1]   SanteDBBre.AddBusinessRule("Patient", "BeforeInsert", [], function(patient) {
[2]
[3]***    patient.tag = patient.tag || {};
[4]       // ensure the rule has not been run
[5]       if(patient.tag["ReviewState"] === undefined)
[6]           patient.tag["ReviewState"] = 'NotReviewed';
[7]       return patient;
[8]
[9]   });
[10]
```

Notice the \*\*\* indicator for the breakpoint. You can also list a series of breakpoints with the breakpoint list command (`bl`).

In order to execute a rule, we first must load a Patient into scope. This can be done with either:

* Set data query (`sdq`) to load a patient from the database
* Set data file (`sfv` , `sfx`, or `sfj`) to load the patient from view model, XML or JSON respectively
* Creating a new patient with set scope (`ss`)

For this tutorial lets set the scope to a new patient:

```
tagme.js (idle) >ss Patient '{ "dateOfBirth":"2017-01-01" }'
tagme.js (idle) >dj
{
  "dateOfBirth": "2017-01-01",
  "language": [],
  "classConcept": "bacd9c6f-3fa9-481e-9636-37457962804d",
  "determinerConcept": "f29f08de-78a7-4a5e-aeaf-7b545ba19a09",
  "relationship": [],
  "$type": "Patient"
}
tageme.js (idle) >
```

Dumping the scope can be done as:

* XML (IMSI format) with dump scope xml (`dx`)
* JSON (IMSI format) with dump scope JSON (`dj`)
* View Model (Applet Format) with dump scope viewmodel (`dv`)

Scope data can be exchange with exchange scope (`xs`), which is useful if you're using the set data query operation to select a single result.

Once we're ready to run a rule, we use the goto rule function (`go.rule`). Because a breakpoint is set on line 3 in BeforeInsert the debugger will break on line 3:

```
tageme.js (idle) >go.rule BeforeInsert
[3]++>    patient.tag = patient.tag || {};
```

At a breakpoint we can print the current block of code with print block (`pb`) to get context of where our breakpoint is (highlighted with +++>)

```
tageme.js @ 3 (step) >pb
[1]   SanteDBBre.AddBusinessRule("Patient", "BeforeInsert", [], function(patient) {
[2]
[3]++>    patient.tag = patient.tag || {};
[4]       // ensure the rule has not been run
[5]       if(patient.tag["ReviewState"] === undefined)
[6]           patient.tag["ReviewState"] = 'NotReviewed';
[7]       return patient;
[8]
```

Our prompt will also show the current line of code (tagme.js @ 3 (step)).

We can use the dump local (`dl`) or dump global (`dg`) to inspect the contents of the local or global JavaScript scope:

```
tageme.js @ 3 (step) >dl
Count:2
[patient] System.Dynamic.ExpandoObject
[arguments] [object Arguments]
```

To get a specific variable contents we dump the object

```
tageme.js @ 3 (step) >dl patient
Count:4
[$type] Patient
[$id] obj0
[dateOfBirth] 1/1/2017 12:00:00 AM
[creationTimeModel] 1/1/0001 12:00:00 AM
```

To increment the program we can use:

* Step over using "go over" (`go`) which will run the line of code and stop
* Step into using "go in" (`gi`) which will run the line of code and break at the first line of a called function
* Go until next breakpoint (`gn`) which will continue to run the program until the next break point is hit
* Step out using "go up" (`gu`) which will execute until the current scope is exited

If we run the rule line by line using `go` we get the following output:

```
tageme.js @ 3 (step) >go
[5]++>    if(patient.tag["ReviewState"] === undefined)
tageme.js @ 5 (step) >go
[6]++>        patient.tag["ReviewState"] = 'NotReviewed';
tageme.js @ 6 (step) >go
[7]++>    return patient;
tageme.js @ 7 (step) >go
tageme.js @ 7 (step) >
Execution Complete, result set to scope
```

The execution of the rule is now complete, if we were to dump the scope we would see our patient object has been updated with our tag:

```
tageme.js (idle) >dj
{
  "dateOfBirth": "2017-01-01",
  "language": [],
  "classConcept": "bacd9c6f-3fa9-481e-9636-37457962804d",
  "determinerConcept": "f29f08de-78a7-4a5e-aeaf-7b545ba19a09",
  "relationship": [],
  "tag": [
    {
      "key": "ReviewState",
      "value": "NotReviewed",
      "$type": "EntityTag"
    }
  ],
  "creationTime": "0001-01-01T00:00:00.0000000-05:00",
  "$type": "Patient"
}
```

We can also debug our validator by running go.validate:

```
tageme.js (idle) >go.validate
tageme.js (run) >Error  Patients must have a gender

Execution Complete
```

Here we can see our validation rule has failed for the currently scoped patient. In the IMS this result in an HTTP 422 error and an OperationResult with that message listed.

### &#x20;More Information

You can find out more information about how to use the debugger with the debugger manual pages.
