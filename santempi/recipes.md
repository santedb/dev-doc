# Recipes

This page contains several "recipes" that you can use to quick start your MPI deployment.

## Generating a New ID

You can easily have SanteMPI generate new identifiers using the built in [Business Rules Engine](../santedb/extending-santedb/applets/business-rules.md).

### Create a new Business Rules File

Create a new JavaScript file in the **rules/** folder of your applet / plugin for SanteMPI. The basic structure of this file should be:

```javascript
/// <reference path="../.ref/js/santedb-bre.js" />
/// <reference path="../.ref/js/santedb-model.js" />
/// <reference path="../.ref/js/santedb.js" />

/**
 * Elbonia MPI / SanteMPI Rules for Generating new ID
 * --
 */

```

### Write Generator Function

Next, write your ID generator in JavaScript, for example, this generator will create a 10 digit random identifier from UUID, and appends a mod 97 check digit to the end:

```javascript
/**
 * @summary Generates an Elbonia Health Card ID
 */
function generateElboniaId() {

    // Use UUID RNG to get a random string
    var source = SanteDBBre.NewGuid().replace(/[a-zA-Z\-]/ig, '').substring(0, 10);
    // Pad to 10 digits
    source = source.pad('0', 10);
    // Convert to an array of digits
    var key = "0123456789";
    var seed = ("0" + source).split('')
             .map(function (c) { 
                 return key.indexOf(c); 
             }).reduce(function (a, v, i) { 
                 return ((a + v) * 10) % 97; 
             });

     // Generate check digit             
     seed *= 10; seed %= 97;
     var checkDigit = (97 - seed + 1) % 97;
     checkDigit += "";

    // Return identifier
     var retVal = source + checkDigit.pad('0', 2);
     return retVal;
};
```

### Write Business Rule

Next, we'll write a small function which accepts a patient as a parameter and adds a new identifier if one has not already been assigned

```javascript
/**
 * @summary Business rule function
 */
function appendPatientID(patient) {

    // Does patient have no identifiers?
    if (!patient.identifier)
        patient.identifier = {};

    // If operating in a server environment
    if (SanteDBBre.Environment == ExecutionEnvironment.Server) {
        // Append ID only an existing one doesn't exist.
        if (!patient.identifier.ELB_HEALTH_ID)
            patient.identifier.ELB_HEALTH_ID= { value: generateElboniaId() };
    }
    return patient;
}
```

### Attach Business Rules to Triggers

Finally, attach the business rule functions to the SanteDB triggers. The example below will attach the append function to the BeforeInsert trigger on PatientMaster

```javascript
// Bind the business rules
SanteDBBre.AddBusinessRule("PatientMaster", "BeforeInsert", { "deceasedDate": "null" }, appendPatientID);
```

### Register the Identifier Generator

You can also have the UI made aware of the presence of this generator by registering an identifier generator.

```javascript
// Add identifier generators
if(SanteDB.application) 
    SanteDB.application.addIdentifierGenerator("ELB_HEALTH_ID", generateElboniaId());
```



