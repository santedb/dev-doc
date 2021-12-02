# Adding Security Policy based on Occupation

In this recipe, we're going to leverage the SanteDB privacy subsystem to flag any patient whose occupation indicates they are a politician with a VIP code and a sensitive information policy. This will allow SanteMPI to hide our politician's information from those users who do not have access to view their sensitive records.

### Dataset

First, we create a dataset which establishes our occupation code for a politician, our security policy for "VIP Data Access Policy".

```markup
<dataset xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" id="Demo Dataset" xmlns="http://santedb.org/data">
  <update skipIfError="true" insertIfNotExists="true">
    <Concept xmlns="http://santedb.org/model">
      <id>ff4fb688-5a91-11eb-ae93-0242ac130002</id>
      <isReadonly>false</isReadonly>
      <mnemonic>OccupationType-ElboniaParliamentarian</mnemonic>
      <statusConcept>c8064cbd-fa06-4530-b430-1a52f1530c27</statusConcept>
      <conceptClass>0d6b3439-c9be-4480-af39-eeb457c052d0</conceptClass>
      <name>
        <language>en</language>
        <value>Parliamentarian of Elbonia</value>
      </name>
      <conceptSet>f76f4eac-487c-11eb-b378-0242ac130002</conceptSet>
    </Concept>
  </update>
  <update insertIfNotExists="true">
    <SecurityPolicy xmlns="http://santedb.org/model">
      <id>e347d512-5f3c-11eb-bec6-00155d640b23</id>
      <name>Health Record of Politician</name>
      <oid>2.25.143743319928604103332532813070351420225</oid>
      <isPublic>true</isPublic>
      <canOverride>false</canOverride>
    </SecurityPolicy>
  </update>
</dataset>
```

### Create a new Business Rules File

Create a new JavaScript file in the **rules/** folder of your applet / plugin for SanteMPI. The basic structure of this file should be:

```javascript
/// <reference path="../.ref/js/santedb-bre.js" />
/// <reference path="../.ref/js/santedb-model.js" />
/// <reference path="../.ref/js/santedb.js" />

/**
 * Elbonia MPI / SanteMPI Rules for protecting policitician's records
 * --
 */

```

### Write Rule Code

Next, you'll want to write some code that flags our parliamentarian .

```javascript
/**
 * Business rule - Flag Parliamentarian
 */
function flagParliamentarian(patient) {

    if(!patient.policy)
    {
        patient.policy = [{ "policy": "e347d512-5f3c-11eb-bec6-00155d640b23", "grant": 0 }];
    }
    else
    {
        patient.policy.push({ "policy": "e347d512-5f3c-11eb-bec6-00155d640b23", "grant": 0 });
    }
    return patient;
}

```

### Attach the Business Rule

Finally, add the business rule to the BeforeInsert and BeforeUpdate method on an incoming patient whose occupation code matches our occupation listed above.

```javascript
SanteDBBre.AddBusinessRule("mpi.vip.occupation.insert", "Patient", "BeforeInsert", { "occupation" : "ff4fb688-5a91-11eb-ae93-0242ac130002" }, flagParliamentarian);
SanteDBBre.AddBusinessRule("mpi.vip.occupation.update", "Patient", "BeforeUpdate", { "occupation" : "ff4fb688-5a91-11eb-ae93-0242ac130002" }, flagParliamentarian);
```
