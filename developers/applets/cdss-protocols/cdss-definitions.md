# CDSS Definitions

Starting with SanteDB 3.0, a new, more robust CDSS XML format has been introduced which greatly improves the re-use of decision logic blocks in CDSS rules. CDSS definitions are contained in an XML structure known as a **CDSS Library**. The CDSS library contains different definition sections as illustrated below.

<figure><img src="../../../.gitbook/assets/image (465).png" alt=""><figcaption></figcaption></figure>

* **Metadata:** Descriptive information about the CDSS library including the version, its current status, and authors, etc.
* **Includes:** Allow a CDSS library to import definitions from other CSS libraries (including the system library)
* **Logic Blocks**: Blocks of definition assets which apply to a particular **context.**
  * **Context:** Allows for the limiting of rules, protocols, and facts to a particular resource type, and even a subset of resource types.
  * **Facts:** Defines a discrete piece of information which is extracted from the context in the CDSS
  * **Rules:** Structures which trigger a series of actions when a series of facts are true
  * **Protocols:** A more structured version of a rule which includes metadata for the CDSS engine, including the steps in a care plan package.
* **Data Blocks:** Allow a CDSS author to include reference data which rules may use. For example, an author may include pre-computed z-scores for a particular type of observation which is then used to set the interpretation of an observation.

The CDSS definition is provided in an XML file, with the structure as illustrated below.

{% hint style="info" %}
You can reference the `SanteDBCdss.xsd` file in your XML editor to obtain auto-complete information for the CDSS definition files.
{% endhint %}

```xml
<CdssLibrary xmlns="http://santedb.org/cdss" 
  uuid="UNIQUE_ID_FOR_LIBRARY" 
  id="dotted_unique_id_for_library" 
  name="human readable name">
  <status>active|trial-use|dont-use|retired</status>
  <meta>
    <!-- metadata here -->
  </meta>
  <!-- Include other libraries' definitions -->
  <include>..</include>
  <!-- Define one or more logic blocks -->
  <logic id="dotted.identifier" name="Human Name for Logic Block">
    <!-- Logic Block Definition -->
  </logic>
  <data id="dotted.identifier" name="Human Name for Data Block">
    <!-- CSV data set -->
  </data>
</CdssLibrary>

```

## Object Status

The status of an object will be used to determine whether the object is to be referenced or used in the evaluation of rules in the library. The status is indicated on an element with `<status>` element on th eobject.

| Status    | Description                                                                                        | Impact                                                                                                                                                                                   |
| --------- | -------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| trial-use | The object is for trial use only.                                                                  | The library, logic block, rule, etc. is only used in debugging and testing contexts.                                                                                                     |
| active    | The object is active and available for system use.                                                 | The library, logic block, rule, etc. is used for all clinical encounters and when the CDSS engine is called.                                                                             |
| retired   | The object was active, and can continue to be used, however should not be used for new care plans. | Patients which have care plans which were generated using the CDSS logic will continue to have the logic applied. However, new care plans will not be generated with this library asset. |
| dont-use  | The object should not be used.                                                                     | Effective immediately (when the state is indicated) no furher proposals will be generated with the assets in the library.                                                                |

## Library Metadata

All library objects carry a metadata section which is used to provide information about the logic block, library, etc.

```xml
<meta>
  <authors>
    <add>Name of a maintainer for the object</add>
  </authors>
  <version>Informative version identifier</version>
  <documentation>Long form documentation for the object which is shown for 
                 administrators and users.</documentation>
</meta>
```

## Logic Blocks

Logic blocks are sections of the CDSS rule file which define one or more facts, rules, protocols, or other computable decision support assets. Logic blocks contain metadata which specify the context to which the contents of the block apply.

Logic blocks are defined with the `<logic>` element, and have a format similar to:

```xml
<logic id="dotted.id.for.logic.block" 
    name="Human Friendly Name For Logic Block"
    uuid="uuid-for-logic-block">
    <status>active|trial-use|dont-use|retired</status>
    <!-- Specify the resource to which all logic in this block applies -->
    <context type="Resource"/>
    <!-- Selectively include the block when the conditions specified are true -->
    <when>
        <!-- Computable Expression Here -->
        <all|any|none|csharp|hdsi/>
    </when>
    <define>
        <!-- One or more definitions -->
    </define>
</logic>
```

### Facts

A fact represents a single piece of information which is known to be true based on data passed to it. A fact represents an instruction which can be used to extract information or make a determination about the state of data. Examples of facts can be:

* The patient's gender
* If the patient is under 5 years old
* If an observation was not made within a time period

A fact is defined with the `<fact>` element, and must carry either an ID or NAME. A fact can be computed using any of the [Computable Expressions](cdss-definitions.md#computable-expressions) documented.

```xml
<fact name="Name of a Fact"
    id="dotted.id.of.fact"
    type="string|integer|long|date|boolean|real">
    <!-- One of -->
    <csharp../>
    <hdsi.../>
    <all.../>
    <none../>
    <!-- Zero or many transforms -->
    <normalize>
        <when>
          <!-- Computable Expression -->
        </when>
        <csharp|hdsi.../>
    </normalize>
</fact>
```

For example, a simple fact that can be defined is whether the patient is female using:

```xml
<fact name="Patient is Female" type="boolean">
    <any>
        <hdsi>genderConcept.mnemonic=Female</hdsi>
        <hdsi>genderConcept=094941e9-a3db-48b5-862c-bc289bd7f86c</hdsi>
    </any>
</fact>
```

Additionally, facts can also be used to extract data in a consistent form, for example, a fact defining the age of the patient in years:

```xml
<fact name="Patient Age In Years" type="real">
  <csharp>DateTime.Now.Subtract(context.Target.DateOfBirth.Value.Date).TotalDays / 365.25f</csharp>
</fact>
```

### Rules

Rules represent a specific case where a series of conditions (facts) are true, the result is one or more actionable proposals or alerts. A rule has a format such as that provided below.

```xml
<rule name="Name of Rule"
      id="dotted.id.of.rule">
      <when>
            <!-- Computable Expression Here -->
            <csharp.../>
            <any.../>
            <hdsi.../>
            <all.../>
            <none.../>
            <fact ref="Name of fact to reference" />
      </when>
      <then>
            <!-- One or More Output Actions Here -->
            <propose.../>
            <raise.../>
            <assign.../>
            <apply ref="Name of another rule to apply"/>
      </then>
</rule>
```

Rules are applied whenever a library is executed, an object is analyzed or when a protocol references them. For example, a rule may raise an alert for the user when a known allergy exists

```xml
<rule name="Raise Alert When Patient Has Reported AEFI to COVID Vaccine">
    <when>
        <all>
            <fact ref="Patient Has Unresolved COVID Vaccine AEFI" />
            <fact ref="Patient Was Proposed COVID Vaccine" />
        </all>
    </when>
    <then>
        <raise>
            <issue xmlns="http://santedb.org/issue" priority="Warning">
            <![CDATA[Patient has previous suspected or confirmed AEFI for COVID vaccinations 
            in their history, please consult patient history]]>
        </raise>
    </then>
</rule>
```

### Protocols

A protocol is a specialized form of a rule. A protocol has identical metadata to a rule, with the exception that a protocol can define one or more encounter scopes to which the protocol applies, and a protocol explicitly marks a rule as an "entry point" for a more complex series of care which result in the creation of a care plan.

Protocols can be used to represent:

* Regular nutritional counseling for patients based on their weight/history
* Regular vaccination recommendations for patients based on their age/history

A protocol **always applies to PATIENT** , protocols cannot be applied to contexts other than PATIENT.

### Computable Expressions

#### \<HDSI> - Health Data Service Interface Query

#### \<CSHARP> - C# Expression

#### \<ANY>&#x20;

#### \<ALL>

#### \<NONE>

#### \<FACT>



### Output Actions

#### \<PROPOSE> - Propose an Action

#### \<ASSIGN> - Change a Property Value

#### \<RAISE> - Raise an Alert

## Data Blocks

