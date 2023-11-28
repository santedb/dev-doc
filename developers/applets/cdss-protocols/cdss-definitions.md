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

## Computable Expressions

Computable expressions are those expressions which are used to:

* Extract data from a resource as the basis for a `fact`
* Determine a boolean logic output for a `when` condition in a `rule` or `protocol` or as a block on a `logic` block.

Computable expressions are made against either the `context` (which is the input data) or the `scopedObject` which is the current action object. The `scopedObject` represents:

* The input context object for facts
* The output object of a proposal

### Health Data Service Interface Query

The Health Data Service Interface Query computable expression uses the [Health Data Service Query](../../service-apis/health-data-service-interface-hdsi/hdsi-query-syntax/) grammar to extract data or make decisions. HDSI queries are encapsulated in the `hdsi()` qualifier in CDSS text file or the `<hdsi>` element in XML.&#x20;

The HDSI expression is either scoped to `context` meaning the input object to the analysis or the `proposal` which is the currently scoped object. HDSI expressions which are `negated` are those which have a NOT() operation applied to them.

{% tabs %}
{% tab title="CDSS" %}
Multiline expression:

```
hdsi($$
   expression
$$ 
   scoped-to (context|proposal) 
   negated
)
```

Singleline expression:

```
hdsi("expression here" scoped-to (context|proposal) negated)
```
{% endtab %}

{% tab title="XML" %}
```
<hdsi scope="context|scopedObject">expression</hdsi>
```
{% endtab %}

{% tab title="Example" %}
```
define fact "Patient Is Over 10 Years Old" type bool as
    csharp(
    $$
        dateOfBirth=:(age)>P10Y
    $$ 
        scoped-to context
    )
end fact
```
{% endtab %}
{% endtabs %}

### C# Expressions

There arise some instances in your decision logic where you must execute more advanced operations such as calculations, date subtraction, and string formatting. The CDSS engine allow the execution of a limited subset of expressions using the C# language. The subset allows for CDSS rule developers to:

* Cast objects from the context as base types or resources
* Perform mathematical operations&#x20;
* Perform Date calculations&#x20;
* Array functions (like `Find`, `FirstOrDefault`, etc.)

The C# expression handler has access to reflection disabled, and late object binding disabled. While this increases the security of the C# expressions, it does mean that all variables must be cast prior to use.

{% tabs %}
{% tab title="CDSS" %}
```
csharp($$
   // C# Code Here
$$)
```
{% endtab %}

{% tab title="XML" %}
```xml
<csharp><![CDATA[ // csharp goes here ]]></csharp>
```
{% endtab %}

{% tab title="Example" %}
```
...
then 
    repeat for 100 iterations track-by index
        csharp($$
            Trace.WriteLine("Iteration {0}", context["index"])
        $$)
    end repeat
end rule
```
{% endtab %}
{% endtabs %}

#### Context Object

The current CDSS context object can be accessed with the `context` variable. `context` can be used to lookup facts and the output of rules which have been (or will be) executed. Context is used in the following manners

| Description                                                  | Example                                                                                                                                                                                                                                |
| ------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Lookup a fact from the current execution context.            | `context["name of fact"]`                                                                                                                                                                                                              |
| Get the value of a fact with a specified type                | <p><code>context.Int("name of fact")</code> <br><code>context.String("name of fact")</code><br><code>context.Real("name of fact")</code><br><code>context.Date("name of fact")</code><br><code>context.Bool("name of fact")</code></p> |
| Lookup a dataset from the context (see )                     | `context.DataSets["name of dataset"]`                                                                                                                                                                                                  |
| Cast a fact as a RIM based object                            | `(Patient)context["name of fact"]`                                                                                                                                                                                                     |
| Access the input object (context's current execution target) | `context.Target.DateOfBirth`                                                                                                                                                                                                           |
| Set a value of a fact on the context                         | `context["name of fact"] = value of fact`                                                                                                                                                                                              |

#### Special Variables

There are other special variables which can be accessed in the C# interpreter including:

* `scopedObject` which is of type `IdentifiedData` and always points to the current "in scope" object. If the C# appears in a fact definition this is the same as `context.Target` , if it appears in a `propose` statement it is the value of the proposal (the object that is being proposed)
* `value` which is used when a   `normalize` computation is written in C#.

### Aggregate Logic Expression

&#x20;There are three aggregate logic expressions which can be used to combine the result of multiple computable expressions. These are identiifed in the table below:

<table><thead><tr><th>Expression</th><th width="128">Logic</th><th>Description</th></tr></thead><tbody><tr><td><code>any(...)</code></td><td>OR</td><td>Returns TRUE when any of the contained facts or statements return TRUE or a non-null value.</td></tr><tr><td><code>all(...)</code></td><td>AND</td><td>Returns TRUE when all of the contained facts or statements return TRUE or a non-null value.</td></tr><tr><td><code>none(...)</code></td><td>NAND</td><td>Returns TRUE only when all of the contained statements are not TRUE or are a null value.</td></tr></tbody></table>

These logic statements can be combined to represent decision logic structures, for example, if we want to define a fact that is true when:

* The Patient is Under 18 Months `AND` received the first dose of an antigen in their 17 months, `OR`
* The Patient is Over 18 Months `AND` has `NOT` received any dose of the antigen&#x20;

```
define fact "Child is Eligible for Accelerated MR Schedule" type bool as
    any(
        all(
            hdsi($$ dateOfBirth=:(age)<P18M $$),
            csharp($$ (int)context["Age of Patient for Dose 1"] > 16 $$)
        ),
        all(
            hdsi($$ dateOfBirth=:(age)>P18M &&),
            none("Patient's Administration of Dose 1")
        )
    )
end fact
```

### Fact References

Facts can be referenced and combined using fact references. In the CDSS text file syntax, this is done by referencing the name of the fact in quotes. In XML this is done using the `<fact ref="Name of Fact"/>` element or `<fact ref="#id.of.fact"/>`.

## Output Actions

Actions are used in rules and protocols as a series of steps which should be taken. These actions can:

* Propose that some action or course of treatment be performed
* Assign a value (such as an interpretation, or flag) on the existing object in scope
* Raise an end-user alert which must be cleared prior to completing the encounter
* Apply another rule or decision tree
* Repeat certain actions for a specified number of iterations or until a condition is true.

### Propose

The propose action is used to emit a proposal onto the current context. A proposal represents an `Act` which should occur (with a [mood code ](../../../santedb/data-and-information-architecture/conceptual-data-model/acts/mood-concepts.md)of `Propose`).

Proposals are represented in CDSS text files with the `propose ... end propose` statement or in XML with `<propose>`. Proposals must carry a `model` (see [models](cdss-definitions.md#models)) and optionally a series of `assign` (see [assign](cdss-definitions.md#assign-a-property-value)) statements to modify the model.

{% tabs %}
{% tab title="CDSS" %}
```
// Using a shared model reference
propose "Descriprive Name for Proposal"
   having model "Name of Model Definition To Use"
   with metadata
      ...
   end metadata
   as
      assign ...
end propose

// Using an inline model 
propose "Descriptive Name for Proposal"
   having model with format (json|xml) as
   $$
      model here
   $$
   with metadata 
       ...
    end metadata
    as
       assign ...
end propose
```
{% endtab %}

{% tab title="XML" %}
```xml
<propose name="Name for Proposal">
    <model ref="Name of Referenced Model">
        <json>
           // JSON for inline model
        </json>
     </model>
     <assign ... />
</propose>
```
{% endtab %}

{% tab title="Example" %}
```
define rule "Propose Supplement for Underweight Patients"  as
   when 
      "Patient Is Underweight"
   then 
      propose "Propose Nutrition Supplement Administration"
         having model "Nutrition Supplement Administration Model"
         as
         assign csharp("DateTime.Now") to actTime
         assign const 1 to doseSequence
      end propose
end rule
```
{% endtab %}
{% endtabs %}

### Assign a Value to Property

Actions can also assign computed, fixed values, or facts to a property on the `scopedObject.` When an assignment exists outside of a `propose` this means the assignment occurs on `context.Target` however within a `propose` the assignment is against the scoped (proposed) object.

Assignments are made using the `assign ... to path` syntax or the `<assign>` element in XML.

{% tabs %}
{% tab title="CDSS" %}
```markup
// Assign C# expression 
assign csharp(...) to property
// Assign HDSI expression
assign hdsi(...) to property
// Assign a fact to property
assign "name of fact" to property
// Assign a fixed value to a property
assign const value to property
```
{% endtab %}

{% tab title="XML" %}
```xml
<assign path="propertyName">
    <csharp ... />
    <hdsi ... />
    <fixed>value</fixed>
    <fact ref="name of fact" />
</assign>
```
{% endtab %}

{% tab title="Example" %}
```
rule "Assign Interpretation Code With Observed Value is Low" as
    when 
        all(
            "Observed Value Is Below Normal Reference Range",
            "Author Has Not Manually Assigned an Interpretation"
        )
    then 
        assign const "6188F821-261F-420C-9520-0DE240A05661" to interpretationConcept
        assign const "true" to tag[cdssInterpretation]
        assign const "CDSS Has Set Interpretation Concept on this observation"
            to note
end rule
```
{% endtab %}
{% endtabs %}

### Raise an Alert

There are often times where a CDSS rule may wish to raise an alert to an end-user in the context of an encounter based on some clinical status of the patient or a previously observed value. This is done with the `raise` statement in CDSS or the `<raise>` element in XML.

The raise alert function will do three things:

1. When the CDSS engine is being called as part of analysis for a captured value (via `Analyze()`) it will be displayed to the user in their encounter capture screen.
2. When the CDSS engine is being called as part of a care plan generation, the issue is added to the care plan in the [http://santedb.org/extensions/core/safetyConcernIssue](http://santedb.org/extensions/core/safetyConcernIssue) extension.
3. When the CDSS engine is being called prior to discharge of the patient, the end user must clear (or acknowledge) the alert before discharging the patient.

{% tabs %}
{% tab title="CDSS" %}
```
raise 
   having priority (danger|warn|info)
   having type "UUID-OF-CONCEPT-FOR-CLASSIFICATION"
   having id <dotted.id.for.issue>
   with metadata
      ...
   end
$$
   This is the text that is to be displayed in the alert. You can also use a 
   single line string with "quotes around a single line of text"
$$ 
```
{% endtab %}

{% tab title="XML" %}
```
<raise>
    <issue xmlns="http://santedb.org/issue"
        priority="Error|Warning|Information"
        id="dotted.id.of.issue"
        type="uuid-of-issue-type"
    >
    This is the text of your issue
    </issue>
</raise>
```
{% endtab %}

{% tab title="Example" %}
```
define rule "Alert Clinician the Nutritional Counseling Should be Performed" as
    when 
        any(
            "Child Is Under Healthy Weight For Age",
            "Child Is Over Healthy Weight for Age"
        )
    then 
        raise having priority warn
            $$
                The observed weight indicates that the child is not a normal 
                healthy weight. Please review pamphlet PM5049 with the guardian 
                prior to discharge.
            $$
end rule
```
{% endtab %}
{% endtabs %}

### Apply Another Rule

One rule may be chained to another via an explicit call. This is useful for protocols where a series of rules needs to be executed in a specific order to create an appropriate care plan. Applying rules is performed via the `apply` statement or `<apply>` in XML.

{% tabs %}
{% tab title="CDSS" %}
```
// Apply by rule name
apply "name of the rule to be applied"
// Apply by rule unique id
apply <dotted.id.of.rule>
```
{% endtab %}

{% tab title="XML" %}
```
<!-- Apply via name -->
<apply ref="Name of Rule to be Applied" />
<!-- Apply via ID -->
<apply ref="#dotted.id.of.rule.to.be.applied" />
```
{% endtab %}

{% tab title="Example" %}
```
define protocol "A simple vaccination protocol" as 
    when 
        "Patient is Eligible for Enrolment to Simple Vaccination Programme"
    then 
        assign "true" to tag[IsEnrolledInSpecialProgramme]
        apply "Simple Vaccination Programme Step 1"
        apply "Simple Vaccination Programme Step 2"
end protocol
```
{% endtab %}
{% endtabs %}

### Repeat Actions

Any action (proposals, assignment, raising, etc.) can be repeated a specific number of iterations (like a for loop) or until a certain fact becomes true or not null (like a while loop). Repeat actions are defined with the `repeat ... end repeat` statements or the `<repeat>` element in XML.

{% tabs %}
{% tab title="CDSS" %}
```
// Repeat specified actiosn N times 
repeat for N iterations track-by fact_name
    apply ...
    propose ...
    raise ...
    assign ...
end repeat

// Repeat specified actions until the specified fact becomes true
repeat until 
    // one of 
    hdsi( ... )
    csharp( ... )
    "fact name"
    all( ... )
    any( ... )
    none( ... )
    // actions
    apply ...
    propose ...
    raise ...
    assign ...
end repeat
```
{% endtab %}

{% tab title="XML" %}
<pre class="language-xml"><code class="lang-xml">&#x3C;!-- Repeat N times -->
&#x3C;repeat iterations="N" trackBy="name_of_track_fact">
<strong>    &#x3C;apply ... />
</strong>    &#x3C;raise ... />
    &#x3C;propose ... />
    &#x3C;assign ... />
&#x3C;/repeat>

&#x3C;!-- Repeat until fact is true -->
&#x3C;repeat>
    &#x3C;until>
        &#x3C;csharp ... />
        &#x3C;hdsi ... />
        &#x3C;all ... />
        &#x3C;any ... />
        &#x3C;none ... />
        &#x3C;fact ref="name of fact" />
    &#x3C;/until>
    &#x3C;apply ... />
    &#x3C;raise ... />
    &#x3C;propose ... />
    &#x3C;assign ... />
&#x3C;/repeat>    
</code></pre>
{% endtab %}

{% tab title="Example" %}
```
define protocol "Measure Weight for 6 months post-operation" 
    when 
        "Patient Has Had Procedure XYZ Performed and Requires Weight Observation"
    then 
        repeat for 6 iterations track-by index
            propose "Weight Observation"
                having model "Weight Observation"
                as 
                assign csharp($$ 
                    ((DateTime)context["Date Of Procedure"]).AddMonths((int)context["index"])
                $$)
            end propose
        end repeat
end protocol            
```
{% endtab %}
{% endtabs %}

## Data Blocks

