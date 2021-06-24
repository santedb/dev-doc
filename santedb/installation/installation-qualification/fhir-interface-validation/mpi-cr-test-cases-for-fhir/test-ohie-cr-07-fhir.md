---
description: Full Patient Registration
---

# TEST: OHIE-CR-07-FHIR

This test ensures that the Client Registry can properly store key fields related to patient demographics fields, and faithfully return them on subsequent queries using the fields stored within the CR.

## References

* [Integrating the Health Enterprise Patient Master Identity Registry](https://www.ihe.net/uploadedFiles/Documents/ITI/IHE_ITI_Suppl_PMIR.pdf)
* [HL7 FHIR RelatedPerson Resource](http://hl7.org/fhir/relatedperson.html)
* [HL7 FHIR Patient Resource](http://hl7.org/fhir/patient.html)
* [Integrating the Health Enterprise Patient Demographics Query for Mobile](https://www.ihe.net/uploadedFiles/Documents/ITI/IHE_ITI_Suppl_PIXm.pdf)

## Discussion

The IHE PDQm transaction is used in scenarios where demographics fields are used to locate candidate demographics entries to/from the client registry's central store. The Client Registry is expected to:

* Be capable of storing all demographics fields in the registration message within this test
* Perform matching on the provided demographics fields with the fields in its data store
* Apply appropriate modifiers to the search query parameters that allow a client to have control over the nature of matching.

## Pre-Conditions

Prior to running this test ensure that the pre-conditions from [TEST: OHIE-CR-02](test-ohie-cr-02-fhir.md#pre-conditions-setup) have been run.

### Create ORGs Domain

The ORG domain is registered to support the identifiers given to organizations in the SanteDB instance. 

```markup
<dataset id="ORG Domain" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://santedb.org/data">
  <!-- TEST -->
  <insert skipIfError="false" skipIfExists="true">
    <AssigningAuthority xmlns="http://santedb.org/model">
      <name>OHIE Organization Domain</name>
      <domainName>ORG</domainName>
      <oid>2.16.840.1.113883.3.72.5.9.20</oid>
      <url>http://ohie.org/test/orgs</url>
      <isUnique>true</isUnique>
    </AssigningAuthority>
  </insert>
</dataset>
```

#### Create PROVIDERs Domain

The providers domain is registered to support the identifiers given to practitioners / providers.

In SanteDB this can be seeded with a dataset: 

```markup
<dataset id="NID Domain" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://santedb.org/data">
  <!-- TEST -->
  <insert skipIfError="false" skipIfExists="true">
    <AssigningAuthority xmlns="http://santedb.org/model">
      <name>OHIE Providers Domain</name>
      <domainName>PROVIDERS</domainName>
      <oid>2.16.840.1.113883.3.72.5.9.21</oid>
      <url>http://ohie.org/test/practs</url>
      <isUnique>true</isUnique>
    </AssigningAuthority>
  </insert>
</dataset>
```

## Authenticate as TEST\_HARNESS

The test harness authenticates against the SanteMPI IdP using a client\_credentials grant for the test-harness.

```http
POST http://sut:8080/auth/oauth2_token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: sut:8080
Content-Length: 112

grant_type=client_credentials&scope=*&client_id=TEST_HARNESS&client_secret=TEST_HARNESS
```

## Register Flynn Full Profile

The test harness will register a patient into the client registry which has a complete demographics profile. The patient resource being registered has the following attributes:

* Identifier `FHR-070` in domain `http://ohie.org/test/test`
* Official Name: Dr. \(Prefix\) Flynn Full \(Given\) Profile \(Surname\) III \(Suffix\)
* Alias: Dr. Profile
* Home Address: Unit 32 \(Line\) 123 Ontario St. \(Line\) , Beamsville \(City\), Lincoln \(District\), Ontario \(State\), Canada \(Country\), L0R2A0 \(Postal Code\)
* Workplace Phone: +12039203
* Home Email: flynn@ohie.org
* Mobile: +10293829343
* Gender: Male
* Birthdate: 1982-03-02
* Marital Status: Married
* Contact:
  * Insurance Company
  * Name: ACME Insurance Corp.
  * Organization: Organization/ohie-cr-07-10-fhir
* Contact:
  * Relationship: Next of Kin / Contact 
  * Name: Allison Profile
  * Address: 123 Ontario St. Beamsville, Lincoln, Ontario, Canada L0R2A0
  * Gender: Female
* Communication: EN \(Preferred\), FR
* General Practitioner: Practitioner/ohie-cr-07-10-fhir
* Managing Organization: Organization/ohie-cr-07-10-fhir-emp

Additionally, the message has registration information for Flynn's insurance provider ACME Insurance, Flynn's Wife Allison Profile, Flynn's Practitioner Dr. Andrew Fudd, and his Managing Organization Good Health Hospital.



