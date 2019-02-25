# Clinical Decision-Support

##  Introduction

This tutorial is intended to assist developers in getting started with the SanteDB Protocol Definition XML format, the format in which SanteDB clinical protocol rules are expressed.

### What is a Clinical Protocol?

In SanteDB, a clinical protocol is defined as a series of actions that must occur to care for a patient based on a series of entry criteria or rules. SanteDB care planning engine will take one or more protocols for a patient to generate a proposed plan of care for that patient.

Each clinical protocol is defined as a separate series of clinical events that must occur, you don't have to worry about bundling them together. For example, if you are writing a series of clinical protocol rules for DTaP and ROTA you could \(and should\) seperate out the domains of that protocol.

### How does SanteDB use these protocols?

Whenever a function calls the CarePlanning service, the SanteDB back end will contact the clinical protocol repository to gather a list of IClinicalProtocol implementations to be executed \(the XML protocol handler is one of these implementations, but there are others\). The care planner then executes the logic in the clinical protocol files asynchronously collecting the results in a CarePlan instance.

If the caller requested that the care planner create proposed encounters \(appointments\) then the care planner will group the proposed actions in the CarePlan as a periodic hull function of the StartTime - Coalesce\(StopTime, ActTime\).

### Understanding MoodConcepts

Before we begin writing our clinical protocols, we first have to understand an often overlooked attribute on all SanteDB objects, the MoodConcept. The MoodConcept is described in more detail in the schema and technical documentation, however it will be summarized here for brevity.

All Acts in SanteDB carry with them a mood concept, this instructs data consumers the mode of the data. The most common mood concept are:

| Mood concept | Description |
| :--- | :--- |
| EventOccurence | Indicates that the act **did** occur, meaning something was actually done to the patient. |
| Intent | Indicates that the act is something that someone **intends** to do in the future |
| Request | Indicates that the act is something that a human is **requesting** be done at a later time |
| Propose | Indicates that the act is something that is being **proposed** to be completed |

For the care planner and clinical protocols, we look to the Propose mood concept, as the computer and our protocols are simply proposed steps in a care plan.

### Setting up your Materials or other required assets

Please note that SanteDB does not treat a vaccination protocol differently than any other clinical protocol. This means that if you ware setting up a clinical protocol which relies on materials, places, or other entities, you must ensure that those entities are created appropriately. This can be done using the user interface, or alternately using a dataset file.

## The CDSS XML Format

Clinical protocols are defined in the `protocols/` directory of an applet. When this applet is uploaded to the IMS, it will install the protocol into the IMS and distribute the protocol to all connected clients.

The protocol XML format is described in the ClinicalProtocol.xsd schema distributed with the SDK and can be used by any standard XML editor to provide code completion. In this tutorial we will be using Microsoft Visual Studio to do this editing.

### Creating your protocol file

For this tutorial, we're going to do protocol for a fake HepA+HepB dualvalent adult schedule which requires three doses. \(Note: This is not medically accurate, and is for illustrative purposes\). The dosing schedule looks like this:

* d1 = p.dob + \('9yr' .. \)
* d2 = d1.time + \('1mo' .. '1yr'\),
* d3 = d2.time + \('1yr' .. '3yr'\)

Basically in human terms:

* Dose 1 can occur anytime after the patient's 9th birthday
* Dose 2 should occur 1 after after dose 1 but is still effective if given up to one year
* Dose 3 should occur 1 year after Dose 1 but is no longer effective if given 3 years after dose 1.

The first thing we will do is create a new XML file in our applet project under `protocols/`. The name can be anything but it is good practice to use the format:

`[jurisdiction].protocol.[type].[class].xml`

Given that, if we're in Elbonia \(our fake jurisdiction\) the filename would be

`el.protocol.vacc.hepabdvalent.xml`

The next thing we want to do \(to make our editing easier\) is to add a reference to the ClinicalProtocol.xsd schema.

We now can create the start of our XML protocol:

```markup
<?xml version="1.0" encoding="utf-8" ?>
<ProtocolDefinition xmlns="http://santedb.org/cdss">
  
</ProtocolDefinition>
```

### Identifying your Protocol

Whenever SanteDB creates an Act based on the suggestion of a clinical protocol, or whenever it is installing your applet, it needs to assign a unique identifier to the protocol for linking. The four attributes that control this behavior are:

*  **id** - The developer friendly name for the protocol like MyProtocol1
*  **name** - The human friendly name for the protocol like HepA+HepB Dualvalent
*  **uuid** - The universally unique name for the protocol \(a UUID\)
*  **version** - The version of the protocol represented in the file.

After adding these your protocol should look like this:

```markup
<ProtocolDefinition xmlns="http://santedb.org/cdss" 
                    id="aa_hebab2valent"
                    name="Elbonia HepA+HepB 3 Dose Standard Schedule"
                    uuid="6DFCA6C8-5934-4D7E-9469-EDBAB3983888"
                    version="1.0.0.0">
```

**Important:** The UUID must be unique. Don't just copy/paste them from examples or other protocols. If you change a protocol you must change the UUID.

### Identifying Entry Criteria

Next, we have to determine who we even want to apply this protocol to. The entry criteria could be:

*  **Mandatory** - In which case we want to define the entry criteria for populations which must have the schedule applied \(for example: All FEMALES must have HPV\)
*  **Optional** - In which case subsequent doses are based off the first.

For our example, we're going to say that this HepA+HepB vaccination is optional. This means that we only want to schedule Dose \#2 and Dose \#3 if Dose \#1 was given.

**Note:** Our dosing schedule says that we can only apply it to patients who are 9 or older, however that is validation rather than planning, so that type of validation rule would go in the business rules JavaScript file to prevent administration of that particular vaccination.

To do this we create a `<when>` tag on our protocol. The WHEN tag can use HDSI expressions or simple LINQ expressions. Our entry criteria is:

* When the patient was involved in a SubstanceAdministration where the product given was this particular type of vaccine
  *  **note**: You can also base your condition on Consumable rather than Product if you care which brand the previous vaccination was
* When the dose sequence of that administration was 1.

```markup
  <when>
    <hdsiExpression>
      participation[RecordTarget].target.participation[Product].target.typeConcept.mnemonic=VaccineType-HepAHepB&amp;
      participation[RecordTarget].target@SubstanceAdministration.sequence=1
    </hdsiExpression>
  </when>
```

If the schedule was mandatory we might do something like this:

```markup
  <when>
    <!-- Patient is 9 years old -->
    <linqExpression>now.Subtract(DateOfBirth.Value.Date).TotalDays &gt;= 3285</linqExpression>
  </when>
```

### Define the rule for Dose \#2

Next we have to define a step in our clinical protocol. This is known as a rule. Rules are expressed in common when/then notation. Again the when clauses can use HDSI query or LINQ to filter.

When we look at our Dose 2 logic it was:

d2 = d1.time + \('1mo' .. '1yr'\),

So we want to say that when:

* The time that the patient **has** received the first dose of the vaccination where
  * The product given was HepA+HepB vaccine, and
  * The dose sequence was 1, and
  * The dose was actually given \(not negated\)
* We also don't want to propose duplicates, so we should also make a rule that the patient **has not** received a vaccination where:
  * The product given was HepA+HepB, and
  * The dose sequence was 1, and
  * The dose was actually given

We could get more fancy to say if they showed up and were explicitly not given Dose \#2 \(i.e. they showed to an appointment but there was a stock out\), or if the patient has a known intolerance we shouldn't schedule this, but for now we'll keep the example simple.

```markup
  <rule id="HEPAB_2" name="HepA+HepB Second Dose">
    <when evaluation="and">
      <!-- Patient DID Receive Dose #1 -->
      <hdsiExpression>
        participation[RecordTarget].target.participation[Product].target.typeConcept.mnemonic=VaccineType-HepAHepB&amp;
        participation[RecordTarget].target@SubstanceAdministration.sequence=1&amp;
        participation[RecordTarget].target.isNegated=false
      </hdsiExpression>
      <!-- Patient DID NOT Receive Dose #2 -->
      <hdsiExpression negationIndicator="true">
        participation[RecordTarget].target.participation[Product].target.typeConcept.mnemonic=VaccineType-HepAHepB&amp;
        participation[RecordTarget].target@SubstanceAdministration.sequence=2&amp;
        participation[RecordTarget].target.isNegated=false
      </hdsiExpression>
    </when>
  </rule>
```

### Define the "then" if Dose \#2 should be proposed

The 'then' logic on a rule indicates what should happen if the "when"condition was successful. Here there are two steps, one where we define a template of something to propose be done, and the other where we set dynamically the properties on that object.

```markup
    <then>
      <action>
        <jsonModel>
          <![CDATA[
            {
              "$type": "SubstanceAdministration",
              templateModel: {
                  mnemonic: "act.substanceadmin.immunization"
              },
              "moodConcept": "ACF7BAF2-221F-4BC2-8116-CEB5165BE079",
              "typeConcept": "F3BE6B88-BC8F-4263-A779-86F21EA10A47",
              "statusConcept" : "c8064cbd-fa06-4530-b430-1a52f1530c27",
              "doseSequence": 2,
              "doseQuantity" : 1.0,
              "doseUnitModel" : {
                "id": "a4fc5c93-31c2-4f87-990e-c5a4e5ea2e76",
                "mnemonic" : "UnitOfMeasure-Dose"
              },
              "routeModel" : {
                "id": "d594f99f-0151-41a0-a359-282ab54683a1",
                "mnemonic": "RouteOfAdministration-IM"
              },
              "siteModel" : {
                "id": "1edc643d-a93a-47ed-8737-06ede53d0e1f",
                "mnemonic": 'Site-RightArm'
              },             
              "participation": {
                "Product": [{
                  "player" : "6CD437C5-E9C2-4259-AA73-6BE768BA3FC0"
                 }]
               }
             }
          ]]>
        </jsonModel>
      </action>
    </then>
```

**Note:** The player of `6CD437C5-E9C2-4259-AA73-6BE768BA3FC0` is a fake UUID, you would substitute a valid material's product key here.

This will setup the static object, now we want to have some logic that will update the start/stop time of the dose based on our previous expression. To do this we use `<assign>`. Be default the current scope of Assign is the same as the when condition \(the patient\) but we need to change this since we'll be setting properties based on dose 1. To do that we need to set the three properties of assign:

*  **propertyName** Which identifies the property in the proposed object we want to change
*  **scope** Which identifies the scope property we want to use
*  **where** Which allows us to filter to a particular object in the scope array

```markup
        </jsonModel>
        <assign scope="Participations" where="participationRole.mnemonic=RecordTarget&amp;source.classConcept=932A3C7E-AD77-450A-8A1F-030FC2855450&amp;source@SubstanceAdministration.doseSequence=1&amp;source.participation[Product].player.typeConcept?.mnemonic=VaccineType-HepAHepB" propertyName="StartTime">Act.ActTime.AddMonths(1)</assign>
        <assign scope="Participations" where="participationRole.mnemonic=RecordTarget&amp;source.classConcept=932A3C7E-AD77-450A-8A1F-030FC2855450&amp;source@SubstanceAdministration.doseSequence=1&amp;source.participation[Product].player.typeConcept?.mnemonic=VaccineType-HepAHepB" propertyName="ActTime">Act.ActTime.AddMonths(1)</assign>
        <assign scope="Participations" where="participationRole.mnemonic=RecordTarget&amp;source.classConcept=932A3C7E-AD77-450A-8A1F-030FC2855450&amp;source@SubstanceAdministration.doseSequence=1&amp;source.participation[Product].player.typeConcept?.mnemonic=VaccineType-HepAHepB" propertyName="StopTime">Act.ActTime.AddMonths(12)</assign>

      </action>
```

## Testing your Protocol

The SanteDB SDK provides a utility for testing your clinical protocols before deploying in production. In order to run the debugging tool, you will need a copy of Minims \(also in the SDK\) database. This allows you to debug your protocols against configured data sources. You can obtain these files by:

* Creating a backup from the SanteDB Disconnected Client mobile application
* Pointing the database at a configured Minims database \(`--db=%localappdata%\minims\openiz.sqlite`\). Note this is the default operating mode when launching the application from the start menu.
* Creating a new database and using anonymous patients \(only recommended for simple protocols\)

This tooling is provided by the SanteDB Debug \(sdb-dbg\) and can be executed by running:

```text
> sdb-dbg --db=newdb1.sqlite --xprot

SanteDB Debugger v1.0.0.20334 (Fredericton)
Copyright (C) 2015-2019 Mohawk College of Applied Arts and Technology
[Warning 2018/01/28 11:41:03] OizDebug.Core.DebugApplicationContext : Can't find the OpenIZ database, will re-install all migrations
Loading debuggees...
Working Directory: C:\Users\justin\Documents
Ready...
dbg >
```

First we want to open our clinical protocol:

```text
dbg >o el.protocol.vacc.hepabdvalent.xml
```

Then we want to test it against a patient. To this we either have to use the scope data query command:

```text
dbg >sdq Patient name.component.value=~Justin
INF: Patient where o => o.Names.Any(name => name.Component.Any(component => (component.Value.Contains("Justin") == True))) (0..)
INF: 1 set to scope
dbg >xs [0]
```

Or, we can load a patient from JSON or XML:

```text
dbg >sfv Patient mypatient.json
```

Or we can create an instance of an anonymous patient:

```text
dbg >ss Patient '{ "dateOfBirth":"2017-01-01" }'
```

Once the scope is set, we can verify the scope by dumping the scope \(ds\) as XML or JSON

```text
dbg >dx
<Patient xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://santedb.org/model">
  <version xsi:nil="true" />
  <sequence xsi:nil="true" />
  <classConcept>bacd9c6f-3fa9-481e-9636-37457962804d</classConcept>
  <determinerConcept>f29f08de-78a7-4a5e-aeaf-7b545ba19a09</determinerConcept>
  <statusConcept xsi:nil="true" />
  <template xsi:nil="true" />
  <dateOfBirth>2017-01-01</dateOfBirth>
  <deceasedDatePrecision xsi:nil="true" />
  <genderConcept xsi:nil="true" />
</Patient>
```

As JSON the command is:

```text
dbg >dj
{
  "dateOfBirth": "2017-01-01",
  "language": [],
  "classConcept": "bacd9c6f-3fa9-481e-9636-37457962804d",
  "determinerConcept": "f29f08de-78a7-4a5e-aeaf-7b545ba19a09",
  "relationship": [],
  "$type": "Patient"
}
```

Now we can run our clinical protocol to see what is generated

```text
dbg >go
Complete result set to scope
```

If you want to look at the care plan generated use either "dump scope" \(`ds`\) or "dump scope as JSON" \(`dv` or `dj`\)

```text
dbg >dj
{
  "target": {
    "dateOfBirth": "2017-01-01",
    "language": [],
    "classConcept": "bacd9c6f-3fa9-481e-9636-37457962804d",
    "determinerConcept": "f29f08de-78a7-4a5e-aeaf-7b545ba19a09",
    "relationship": [],
    "$type": "Patient"
  },
  "act": [
    {
      "$type": "OpenIZ.Core.Model.Acts.SubstanceAdministration, OpenIZ.Core.Model",
      "route": "d594f99f-0151-41a0-a359-282ab54683a1",
```

