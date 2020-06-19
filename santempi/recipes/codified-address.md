# Codified Address

This recipe will show you how to take free-form addresses from any inbound source \(HL7, API, FHIR, etc.\) and append a CensusTract code to the address. You can also use this same pattern to correct spellings, cross-reference address information, etc.

### Create a new Business Rules File

Create a new JavaScript file in the **rules/** folder of your applet / plugin for SanteMPI. The basic structure of this file should be:

```javascript
/// <reference path="../.ref/js/santedb-bre.js" />
/// <reference path="../.ref/js/santedb-model.js" />
/// <reference path="../.ref/js/santedb.js" />

/**
 * Elbonia MPI / SanteMPI Rules for Codifying Address
 * --
 */

```

### Write Address Lookup Function

Next, write the address lookup function. This function illustrates using the codified address hierarchy in SanteDB and mapping that to the EntityAddress received.

```javascript

/**
 * Business rule - Add address information
 */
function appendAddress(patient) {

     // Fill out addresses  
     if (patient.address) {
        // Use the reflector tool instead of Object.keys here
        var keys = reflector.properties(patient.address);
        
        // Iterate over the types of addresses
        for (var k in keys) {
            var addrType = keys[k];
            var addr = patient.address[addrType];
            if (addr.component) { // address has component
                var censusTract = addr.component.CensusTract;
                if (censusTract) continue; // already has census tract

                // Lookup the place by address components
                var att = 0;

                // Attempt to search for places with the same name - search up the hierarchy
                while (!addr.component.CensusTract && att < 3) {
                    var query = {
                        "_count": 2
                    };

                    if (addr.component.State && att < 3) { // attempt state res
                        query["address.component[State].value"] = addr.component.State;
                        query["classConcept.mnemonic"] = 'State';
                    }
                    if (addr.component.County && att < 2) { // attempt township res
                        query["address.component[County].value"] = addr.component.County;
                        query["classConcept.mnemonic"] = 'County';
                    }
                    if (addr.component.City && att < 1 && addr.component.City != "?") { // attempt full res
                        query["address.component[City].value"] = addr.component.City;
                        query["classConcept.mnemonic"] = 'City';
                    }
                    att++;
                    try {
                        var r = SanteDB.resources.place.find(query);
                        if (r.totalResults == 1 && r.resource && r.resource.length == 1) {
                            var correctAddr = r.resource[0].address['Direct'];
                            if (correctAddr != null)
                                addr.component.CensusTract = correctAddr.component.CensusTract;
                        }
                    } catch(e) {
                        console.error("Error correcting address: " + e);
                    };
                }
            }
        }
    }
    return patient;
}
```

### Attach the Business Rule

Finally, add the business rule to the BeforeInsert method on the patient.

```javascript
SanteDBBre.AddBusinessRule("Patient", "BeforeInsert", { "deceasedDate" : "null"}, appendAddress);
```

