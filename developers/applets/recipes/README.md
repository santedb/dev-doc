# Recipes

This page contains several "recipes" that you can use to quick start your MPI deployment.

## [Generate a Unique Identifier](generating-id-on-registration.md)

You can generate a new unique identifier for any patient (or other entity for that matter) registered in the SanteMPI solution, regardless of where the registration request originated from (HL7, FHIR, API, UI, etc.).&#x20;

## [Codified Address Lookup](codified-address.md)

You can correct addresses being stored in the SanteMPI instance and/or append codified information to the address whenever a registration or update occurs.&#x20;

## [Add Relationship to System/Facility](assigning-a-home-facility.md)

If you're using the disconnected gateway you can write a business rule which will add a relationship to any data configured in the system or facility. You might want to do this, for example, if you're tracking where a patient's "home facility" is.
