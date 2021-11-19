# Extended Data

The SanteDB CDR requires that any data provided to it by callers conform to the logical information either in XML, JSON or ViewModel formats.&#x20;

If you need to store data which cannot be captured in the primary information model you can add it with either an extension or a tag.

## Extensions

Extensions are versioned pieces of information which semantically change or modify the data structure, or capture complex data which changes over time. Extensions:

* Must have a registered extension type (a valid extension type UUID)
* Have effective/obsolete dates which means that they are subject to versioning and may need pruning
* Store the extension valid as a serialized BLOB

### Extension Data Type

SanteDB provides several built-in serializers for handling extension data which are used based on the type of data you'll be storing. SanteDB extension data types included within the solution are:

| Data Type | Handler                    | Description                                         |
| --------- | -------------------------- | --------------------------------------------------- |
| Binary    | BinaryExtensionHandler     | Stores a variable length byte array as a blob       |
| Boolean   | BooleanExtensionHandler    | Stores a 1 byte representation of a binary value    |
| Date      | DateExtensionHandler       | 64-bit (8 byte) ticks from UTC of the time stored   |
| Decimal   | DecimalExtensionHandler    | 128-bit (16 byte) decimal number                    |
| Dynamic   | DictionaryExtensionHandler | A JSON structure of any data object                 |
| Reference | ReferenceExtensionHandler  | A 128-bit UUID pointer to an Entity, Act or Concept |
| String    | StringExtensionHandler     | A variable length string stored in the database     |
| Uuid      | UuidExtensionHandler       | A 128-bit byte array representing a UUID            |

You can create additional extension data types by implementing the `IExtensionHandler` interface in a .NET plugin.&#x20;

### Extension Type Registration

SanteDB provides built extension types which are enumerated below.

{% hint style="info" %}
All extensions are in the http://santedb.org/extensions URL base.
{% endhint %}

| URL                                      | Type       | Use                                                                                           |
| ---------------------------------------- | ---------- | --------------------------------------------------------------------------------------------- |
| /core/jpegPhoto                          | Binary     | Stores a JPG photograph of an entity/act                                                      |
| /core/originalDate                       | Date       | Stores the original or amended date an action was supposed to occur.                          |
| /core/contactRole                        | Dictionary |                                                                                               |
| /core/detectedIssue                      | Dictionary | A structured list of business rules/data quality issues that were detected with an object.    |
| /stock/contrib/gs1/estimatedDeliveryDate | Date       | The original time (from the sender of a GS1 message) of estimated delivery date of an object. |
| /stock/contrib/gs1/shipmentDate          | Date       | The original shipment date of an action                                                       |
| /stock/contrib/gs1/packgingType          | String     | The type of packaging (crate, box, etc.) from the GS1 sender                                  |

You can register your own extensions by using the [HDSI interface](../../../../developers/service-apis/health-data-service-interface-hdsi/) and POSTing a new ExtensionType resource.

## Tags

Tags are another extension point which can be used to attach metadata to an object during processing, disclosure, or to control some operational process. Tags are not versioned and live throughout the lifetime of the object. Tags can be removed and updated, however the history of these changes are not tracked.

Tags require no formal definition of the tag type, and represent a simple key/value pair on the object.&#x20;

{% hint style="info" %}
Tag keys starting with $ are transient, meaning they aren't persisted to the database and are intended to control operational processes within the CDR and its plugins/business rules.
{% endhint %}

### SanteDB Core Tags&#x20;

SanteDB's core plugins affix tags to objects based on the plugins enabled and the status of the object. These tags are described below.

| Tag            | Values                                                                       | Use                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| -------------- | ---------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| $mdm.type      | <p>M = Master</p><p>L = Local</p><p>T = Record of Truth</p><p>O = Orphan</p> | <p>The MDM service uses the type tagging to convey the type <br>of master data record being provided. It is also used by </p><p>callers to instruct the MDM record to perform certain <br>behaviors. For example, sending an update with $mdm.type</p><p>of T would instruct the MDM layer that the resource being</p><p>pushed is a designated record of truth.</p>                                                                                                                                      |
| $mdm.processed | True \| False                                                                | <p>Indicates that the MDM layer has already processed the </p><p>object. This prevents duplicate processing of records.</p>                                                                                                                                                                                                                                                                                                                                                                               |
| $mdm.resource  | Patient \| Place ..                                                          | <p>Indicates the original type of resource the MDM record is</p><p>conveying. This is because MDM Masters are generic Entity</p><p>or Act resources with no clearly identified type. The <br>$mdm.resource tag allows callers to understand the original</p><p>type of data the master is representing</p>                                                                                                                                                                                                |
| $generated     | True \| False                                                                | <p>When retrieving data that was synthesized from other data</p><p>records this flag will be TRUE. This indicates that the result</p><p>is not an *actual* record, rather it is combined from multiple</p><p>local records.</p>                                                                                                                                                                                                                                                                           |
| $alt.keys      | UUID List                                                                    | <p>A list of other keys which the resource references may use.</p><p>Deprecated.</p>                                                                                                                                                                                                                                                                                                                                                                                                                      |
| $pep.masked    | True \| False                                                                | <p>When present in a resource, informs the caller that the </p><p>PolicyEnforcementService or PrivacyEnforcementService</p><p>has masked/redacted or removed sensitive data from the<br>resource returned. This is an indicator to the caller that they</p><p>may need to perform an elevation to unlock all the data. </p><p><strong>Note</strong>: If the PEP is set to HIDE sensitive data then the <br>resource is not returned in any disclosures, and the <br>$pep.masked flag will not appear.</p> |
| $pep.method    | hash \| hide \| redact                                                       | <p>When present in a resource, informs the caller that the policy </p><p>enforcement service took destructive action on the resource </p><p>using the specified privacy enforcement method.</p><p><strong>Note: </strong>The $pep.method of hide on a resource indicates <br>that part of the resource was hidden (usually identifiers)</p><p>if the entire resource is hidden, then the tag wouldn't appear</p><p>on a resource tag.</p>                                                                 |
| $bre.error     | String                                                                       | <p>Used by the BRE engine to convey non-fatal errors to </p><p>callers. This is used for diagnosing / logging and catching</p><p>upstream errors in business rules.</p>                                                                                                                                                                                                                                                                                                                                   |
| $sys.reclass   | True \| False                                                                | <p>Used by the persistence layer to determine whether an <br>object is being re-classified (having its type changed). </p><p>Normally this would cause an error in the persistence layer</p><p>however setting $sys.reclass=true instructs the persistence</p><p>layer to change the object's class. This is how, for example,</p><p>a Person may be re-classified as a Patient.</p>                                                                                                                      |
