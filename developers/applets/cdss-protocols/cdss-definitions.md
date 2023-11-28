# CDSS Definitions

Starting with SanteDB 3.0, a new, more robust CDSS XML format has been introduced which greatly improves the re-use of decision logic blocks in CDSS rules. CDSS definitions are contained in an XML or text file structure known as a **CDSS Library**. The CDSS library contains different definition sections as illustrated below.

<figure><img src="../../../.gitbook/assets/image (465).png" alt=""><figcaption></figcaption></figure>

* **Metadata:** Descriptive information about the CDSS library including the version, its current status, and authors, etc.
* **Includes:** Allow a CDSS library to import definitions from other CSS libraries (including the system library)
* **Logic Blocks**: Blocks of definition assets which apply to a particular **context.**
  * **Context:** Allows for the limiting of rules, protocols, and facts to a particular resource type, and even a subset of resource types.
  * **Facts:** Defines a discrete piece of information which is extracted from the context in the CDSS
  * **Rules:** Structures which trigger a series of actions when a series of facts are true
  * **Protocols:** A more structured version of a rule which includes metadata for the CDSS engine, including the steps in a care plan package.
* **Data Blocks:** Allow a CDSS author to include reference data which rules may use. For example, an author may include pre-computed z-scores for a particular type of observation which is then used to set the interpretation of an observation.

CDSS definitions are transpiled into an XML format from the CDSS source files. The CDSS source files are text files which can be created with any text editor. CDSS library definitions are uploaded to the SanteDB server or loaded into the SanteDB business rules debugger.

The structure of the CDSS and its equivalent XML structure are provided below.

{% tabs %}
{% tab title="CDSS" %}
```
include <id.of.lib.to.include>

define library "name of library file"
   having id <id.of.library>
   having uuid "uuid-of-library"
   having status active|trial-use|retired|dont-use
   with metadata
   ...
   end metadata
as 
   define logic "name of logic block"
      // logic definitions
   end logic
   
   define data "name of data block"
      // CSV data
   end data 
end library
```
{% endtab %}
{% endtabs %}

CDSS files are always placed in the `protocols/` folder of your applet. This folder can contain XML or text-based definitions for your libraries.

## CDSS Library Syntax

### Strings

There are two types of strings which are supported in the CDSS definition file, a single line string is enclosed in double quotes such as `"This is a string"`, a string can be escaped with a double quote such as `"This is a ""string"" that is escaped".`&#x20;

Strings which cross multiple lines or strings which need to use lots of quotes (which would require a lot of escaping) are represented as multi-line strings. These strings are enclosed in `$$` indicators such as `$$ This is a "string" too $$` , these are useful for representing C#, HDSI or even large JSON objects such as:&#x20;

```
$$
{
   "$type": "Patient",
   "dateOfBirth": "2023-01-01"
}
$$
```

### Dotted Identifiers

Dotted identifiers allow for direct, unambiguous references to objects in the CDSS subsystem. Dotted identifiers are enclosed in `<` marks. The use of these are illustrated in references such as `include <org.santedb.example>` where `org.santedb.example` is the dotted identifier.

### Block Definitions

Block definitions include all of: libraries, logic, data, facts, protocols, rules, models, proposals, etc. Blocks are multiple lines which encapsulate the modifiers and instructions for the blocks. Block definitions always have the pattern:

```
define (library|logic|data|fact|model|...) "NAME"
   having statements
   with metadata
       // contents of metadata
   end metadata
   as
      // contents of the block
end (library|logic|data|fact|model...)
```

### Comments

Comments can be added to any of part of your CDSS file. Comments differ from metadata documentation in that comments are stripped from the transpiled source, and are only visible to developers. Any line or part of line following a double-slash `//` is a comment.

### Object Status

The status of an object will be used to determine whether the object is to be referenced or used in the evaluation of rules in the library. The status is indicated on an element with `<status>` element on the object.

| Status    | Description                                                                                        | Impact                                                                                                                                                                                   |
| --------- | -------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| trial-use | The object is for trial use only.                                                                  | The library, logic block, rule, etc. is only used in debugging and testing contexts.                                                                                                     |
| active    | The object is active and available for system use.                                                 | The library, logic block, rule, etc. is used for all clinical encounters and when the CDSS engine is called.                                                                             |
| retired   | The object was active, and can continue to be used, however should not be used for new care plans. | Patients which have care plans which were generated using the CDSS logic will continue to have the logic applied. However, new care plans will not be generated with this library asset. |
| dont-use  | The object should not be used.                                                                     | Effective immediately (when the state is indicated) no furher proposals will be generated with the assets in the library.                                                                |

### Metadata

All library objects carry a metadata section which is used to provide information about the logic block, library, etc. Metadata is placed onto an object using the `with metadata` indicator or in the `<meta>` element.

{% tabs %}
{% tab title="CDSS" %}
```
with metadata
    author The Name of an Author
    author The Name of another Author
    version semantic-version
    doc A line of documentation
    doc another line of documentation
end metadata
```
{% endtab %}

{% tab title="XML" %}
<pre class="language-xml"><code class="lang-xml"><strong>&#x3C;meta>
</strong>  &#x3C;authors>
    &#x3C;add>Name of a maintainer for the object&#x3C;/add>
  &#x3C;/authors>
  &#x3C;version>Informative version identifier&#x3C;/version>
  &#x3C;documentation>Long form documentation for the object which is shown for 
                 administrators and users.&#x3C;/documentation>
&#x3C;/meta>
</code></pre>
{% endtab %}

{% tab title="Example" %}
```
define logic "Example Logic Block"
   having id <org.example.logic>
   having status active
   with metadata
      author An Example Author
      version 1.0-alpha
      doc This is just an example logic block
   end metadata
   ...
end logic
```
{% endtab %}
{% endtabs %}

## Logic Blocks

Logic blocks are sections of the CDSS rule file which define one or more facts, rules, protocols, or other computable decision support assets. Logic blocks contain metadata which specify the context to which the contents of the block apply.&#x20;

Logic blocks have the following contents:

* Context: The object/resource to which the contents of the logic block applies
* When Block: Which is used to further restrict the type of objects to which the logic block applies (for example, only apply to Female patients)
* Definitions: Which are the facts, models, rules, and protocols of the logic block.

Logic blocks are defined with `define logic ... end logic` or the `<logic>` element, and have a format as illustrated below:

{% tabs %}
{% tab title="CDSS" %}
```
define logic "Name of Logic Block"
   having id <dotted.id.of.the.logic.block>
   having uuid "uuid-of-the-block"
   having oid "oid.of.logic.block"
   having status active|trial|dont-use|retired
   having context (Patient|Act|QuantityObservation...)
        when computable_expression
   with metadata
      ...
   end metadata
   as 
      define (fact|model|rule|protocol)
      ..
      end
end logic
```
{% endtab %}

{% tab title="XML" %}
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
{% endtab %}

{% tab title="Example" %}
```
include <org.santedb.core>

library "Example Library"
    having id <org.example.library>
    as 
    
   define logic "Example Logic Block for Female Patients"
       having id <org.example.library.logic.female>
       having context Patient when hdsi("genderConcept.mnemonic=Female")
   as 
       ...
   end logic
end library
```
{% endtab %}
{% endtabs %}

### Facts

A fact represents a single piece of information which is known to be true based on data passed to it. A fact represents an instruction which can be used to extract information or make a determination about the state of data. Examples of facts can be:

* The patient's gender
* If the patient is under 5 years old
* If an observation was not made within a time period

A fact is defined with the `define fact ... end fact` or XML element `<fact>` , and must carry either an ID or NAME. A fact can be computed using any of the [Computable Expressions](cdss-definitions.md#computable-expressions) documented.

{% tabs %}
{% tab title="CDSS" %}
```
define fact "name of fact"
   having id <id.of.fact>
   having type (int|real|bool|string|date)
   having negation (true|false)
   as 
      computable expression
end fact
```
{% endtab %}

{% tab title="XML" %}
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
{% endtab %}

{% tab title="Example" %}
```
library "Example Library"
  as
    ...
    
   define logic "Example Logic Block for Female Patients"
    ...
   as 
     define fact "Patient Is Too Young for HPV Programme"
       having type bool
       with metadata
         doc Patients under 9 years old are too young to receive HPV dose
       end metadata
       as
         hdsi($$ 
           dateOfBirth=:(age)<P9Y
         $$)
     end fact
   end logic
end library
```
{% endtab %}
{% endtabs %}

Facts can also be used to extract data in a consistent form, for example, a fact defining the age of the patient in years may be defined as:

```xml
define fact "Patient Age In Years" having type real as
  csharp($$
     DateTime.Now.Subtract(context.Target.DateOfBirth.Value.Date).TotalDays / 365.25f
  $$)
end
```

#### Normalization

Facts can be normalized according to one or more normalization rules. Normalization is useful when you need a fact to be translated from one format to another using a computation. Take, for example, a rule which may need to determine if an observation made was out of range, however needs to change units (for example weight). Such a fact should be normalized, for example:

```
define logic "Interpret Weight"
    having context QuantityObservation 
        when hdsi("typeConcept=a261f8cd-69b0-49aa-91f4-e6d3e5c612ed")
    as 
    
        // Determine whether the observation was recorded in LBS
	define fact "Weight is Expressed in Lbs" having type bool
        as 
            hdsi("unitOfMeasure=49974584-7c48-457e-a79c-031cdd62714a")
        end fact
        
        // Create a fact which normalizes the wieght into KGs so we can do a lookup
        define fact "Observed Weight Expressed in Kgs" having type real
	as 
	    hdsi("value")
	    normalize when "Weight is Expressed in Lbs" 
	        computed as csharp($$ value * 0.45359237d $$)
	end fact
end logic
```

### Models

Models are used when you wish to define a template of data which is reused. These are usually referenced from proposals, and they represent a fact which has a static, complex structure. Models are defined in the logic block with `define model ... end model` or the `<model>` element in XML.

{% tabs %}
{% tab title="CDSS" %}
```
define model "Name of Model"
    having id <id.of.model>
    having uuid "uuid-of-model"
    having format json|xml
    with metadata
        ...
    end metadata
    as 
    $$
        // contents of the model 
    $$
end model
```
{% endtab %}

{% tab title="XML" %}
```xml
<model name="Name of Model" id="id.of.model">
    <json><![CDATA[.....]]></json>
    <Act|QuantityObservation|CodedObservation.... xmlns="http://santedb.org/model">
        ...
    </Act|QuantityObservation|CodedObservation...>
</model>
```
{% endtab %}

{% tab title="Example" %}
```
define model "Propose HPV Dose Administration"
    having format json 
    as 
    $$
    {
      "$type": "SubstanceAdministration",
      "typeConcept": "F3BE6B88-BC8F-4263-A779-86F21EA10A47",
      "statusConcept" : "c8064cbd-fa06-4530-b430-1a52f1530c27", 
      "doseQuantity" : 1.0,
      "doseUnit" : "a4fc5c93-31c2-4f87-990e-c5a4e5ea2e76",
      "route" : "d594f99f-0151-41a0-a359-282ab54683a1",
      "site" : "dd5db8ed-0d97-4728-bd94-27aacd79ea02",
      "participation": {
	   "Product": [{
              "player" : "15b42b90-17fa-48cd-8121-f909c9d00ccc",
              "quantity": 1
            }]
      }
    }
    $$
end model
```
{% endtab %}
{% endtabs %}

### Rules

Rules are defined within a logic blocks and represent a simple logic construct using when/then semantics. Rules are defined using the `define rule ... end rule` or the `<rule>` element in XML. The when block represents the trigger and is comprised of any [computable expression](cdss-definitions.md#computable-expressions). The then block is a collection of [output actions ](cdss-definitions.md#output-actions)which should be undertaken when the condition is true.

The structure of the rules is illustrated below.

{% tabs %}
{% tab title="CDSS" %}
```
rule "Name of Rule"
   having id <dotted.id.of.rule>
   having uuid "uuid-of-rule"
   having oid "dotted.oid.of.rule"
   having status (active|trial-use|dont-use|retired)
   having priority NNN
   with metadata
      ...
   end metadata
   as 
      when 
         any( ...
         all( ...
         none( ...
         csharp( ...
         hdsi( ...
      then 
         raise ...
         repeat ...
         apply ...
         propose ...
         assign ...
end rule
```
{% endtab %}

{% tab title="XML" %}
```xml
<rule name="Name of Rule"
      id="dotted.id.of.rule"
      priority="n">
      <meta>
          ...
      </meta>
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
{% endtab %}

{% tab title="Example" %}
```xml
define rule "Raise Alert When Patient Has AEFI to COVID Vaccine"
   metadata
     doc Will raise a warning when a COVID vaccination has been proposed and 
     doc an unresolved adverse event or allergy has been recorded
   end metadata
   when 
     all(
       "Patient Has Unresolved COVID Vaccine AEFI",
       "Patient Was Proposed COVID Vaccine"
     )
   then 
     raise $$
       Patient has previous suspected or confirmed adverse reaction or allergy
       to COVID vaccination in their history. Please review allergen and event
       history with patient prior to administration
     $$ having priority danger
end rule
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
When the CDSS engine's `Execute()` or `Analyze()` methods are invoked, all rules which are contained in the relevant logic blocks (which apply to the object being executed or analyzed). Rules are selectively applied when a `ComputeProposal()` call or `GenerateCarePlan()` methods are called based on the protocols which apply.
{% endhint %}

### Protocols

A protocol is a specialized form of a rule. A protocol has identical metadata to a rule, with the exception that a protocol can define one or more encounter scopes to which the protocol applies, and a protocol explicitly marks a rule as an "entry point" for a more complex series of care which result in the creation of a care plan.

Protocols can be used to represent:

* Regular nutritional counseling for patients based on their weight/history
* Regular vaccination recommendations for patients based on their age/history

A protocol **always applies to PATIENT** , protocols cannot be applied to contexts other than PATIENT.

Protocols are defined with the `define protocol ... end protocol` or `<protocol>` element.

{% tabs %}
{% tab title="CDSS" %}
```
define protocol "Name of Protocol"
   having id <dotted.id.of.protocol>
   having uuid "uuid-of-rule"
   having oid "dotted.oid.of.rule"
   having status (active|trial-use|dont-use|retired)
   having priority NNN
   having scope <dotted.id.of.scope>
   having scope "name of scope"
   with metadata
      ...
   end metadata
   as
     when 
       any( ...
       all( ...
       none( ...
       csharp( ...
       hdsi( ...
     then
       raise ...
       repeat ...
       apply ...
       propose ...
       assign ...
end protocol    
```
{% endtab %}

{% tab title="XML" %}
```xml
<protocol name="Name of Rule"
   oid="dotted.oid.of.rule"
   id="dotted.id.of.rule"
   uuid="uuid-of-rule"
   priority="N">
   <scopes>
      <add id="dotted.id.of.scope" oid="oid.of.scope" />
   </scopes>
   <when>
      <csharp ... />
      <hdsi ... />
      <all ... />
      <any ... />
      <none ... />
      <fact ref="name of fact" />
   </when>
   <then>
      <propose ... />
      <assign ... />
      <repeat ... />
      <apply ... />
      <raise ... />
   </then>
</rule>
```
{% endtab %}

{% tab title="Example" %}
```
define protocol "COVID Vaccination Base Immunization Schedule"
    having id <org.example.covid.vaccine.protocol>
    having oid "2.25.30239238239232"
    having scope <org.santedb.emr.enc.adult.consult>
as
    when 
        none(
            "Patient Has Previous Adverse Event to COVID Vaccine",
            "Patient Has No Previous Doses of COVID Vaccine"
        )
    then
        apply "Propose COVID Vaccine Dose #1 Standard Schedule"
        apply "Propose COVID Vaccine Dose #2 Standard Schedule"
end protocol
```
{% endtab %}
{% endtabs %}

### Computable Expressions

#### Health Data Service Interface Query

#### C# Expression

#### Any Contained Expression&#x20;

#### All Contained Expressions

#### No Contained Expressions

#### Fact References



### Output Actions

#### Propose an Action

#### Assign a Property Value

#### Raise an Alert

#### Apply Another Rule

#### Repeat Actions

## Data Blocks

