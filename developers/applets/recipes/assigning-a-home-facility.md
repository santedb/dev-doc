# Assigning a Home Facility

When using the Disconnected Gateway, dCDR Android or dCDR Windows/Linux applications, you can optionally append the "home facility" or "registering facility" to the patient being registered.&#x20;

This pattern works for assigning any relationships you like (for example, automatically assigning birthplace on a birth notification).

### Create a new Business Rules File

Create a new JavaScript file in the **rules/** folder of your applet / plugin for SanteMPI. The basic structure of this file should be:

```javascript
/// <reference path="../.ref/js/santedb-bre.js" />
/// <reference path="../.ref/js/santedb-model.js" />
/// <reference path="../.ref/js/santedb.js" />

/**
 * Elbonia MPI / SanteMPI Rules for Assigning Facility
 * --
 */

```

### Write Assignment Code

Next, you'll want to write some code that looks up the configured facility where the dCDR is running and appends that information to the patient if not already done so.

```javascript
/**
 * Business rule - Append facility on registration
 */
function appendRegisteringFacility(patient) {

    // Only run when not running in master server
    if (SanteDBBre.Environment != ExecutionEnvironment.Server) {
        
        // Prepare relationship
        try {
            if (!patient.relationship)
                patient.relationship = {};

            // Get the configured facilities
            var facility = SanteDBDcg.GetFacilities().resource[0];
          
            // Assign the facility as the SDL
            patient.relationship.ServiceDeliveryLocation = new EntityRelationship({
                target: facility.id
            });
        }
        catch (e) {
            console.error("Error assigning facility: " + e);
        }
    }

    return patient;
};
```

### Attach the Business Rule

Finally, add the business rule to the BeforeInsert method on the patient.

```javascript
SanteDBBre.AddBusinessRule("elb.rule.home_fac", "Patient", "BeforeInsert", { "deceasedDate" : "null"}, appendRegisteringFacility);
```
