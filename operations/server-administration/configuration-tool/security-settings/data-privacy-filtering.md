# Data Privacy Filtering

The `Data Privacy Filtering` panel controls the configuration of the data privacy services in SanteDB. Data privacy services allow administrators to:

* Control how sensitive data is handled in SanteDB iCDR
* Control which resources have specific privacy sensitivity in SanteDB iCDR
* Control how sensitive records are disclosed or updated
* Control which properties on which resources are forbidden (and will result in a privacy violation exception when collected, or queried).

![](<../../../../.gitbook/assets/image (439) (1) (1).png>)

| Option         | Description                                                                                                                           | Example                                                    |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------- |
| Default Action | The action which should be applied to all resources which have been flagged as sensitive, where no specific policy has been assigned. | See: [Policy Actions](data-privacy-filtering.md#undefined) |
| Resources      | The resources which are to be protected with specialized policy enforcement.                                                          |                                                            |

## Resource Controls

Expanding the resources input allows administrators to specify resources in the RIM which are subject to special protections. Clicking the ellipsis on the resources property will open a collection editor change the settings for resource controls:

![](<../../../../.gitbook/assets/image (426) (1) (1).png>)

| Option        | Description                                                                                                                                       | Example                                                                          |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| Action        | The action to be applied on resources which have privacy policies applied to them, when the requesting user does not have a grant for the policy. | See: [Policy Actions](data-privacy-filtering.md#undefined)                       |
| Resource Type | The type of resource that the policy applies to.                                                                                                  | Patient, Person, etc.                                                            |
| Fields        | The properties which are forbidden or have specialized sub-policy enforcement instructions.                                                       | See: [#property-policies](data-privacy-filtering.md#property-policies "mention") |

{% hint style="info" %}
You can set policies on identifiers (on entities and acts) by controlling the policy on `AssigningAuthority`.
{% endhint %}

## Property Policies

The property policies allow implementing jurisdictions to control which properties in which resources are forbidden. Examples of this functionality are:

* Restricting the collection, disclosure, or querying of Patient religion or ethnicity to all users
* Restricting the disclosure, collection or querying of Patient VIP status to only users which have "Access to Taboo Information" policy.

![](<../../../../.gitbook/assets/image (442) (1).png>)

| Option   | Description                                                                                   | Example                                                    |
| -------- | --------------------------------------------------------------------------------------------- | ---------------------------------------------------------- |
| Action   | The action to apply when the caller attempts to access, query, or write data to the field.    | See: [Policy Actions](data-privacy-filtering.md#undefined) |
| Policy   | The policy OIDs which the user must posses in order for the Action not to result in an error. | 2.25.0303030                                               |
| Property | The HDSI property path (root paths only) on the resource, where this policy applies.          |                                                            |

## Policy Actions

Resources, properties and the default policy actions dictate how the privacy filtering engine will handle data whenever:

* The requesting principal lacks appropriate policy permissions to view data (when flagged), or
* The requesting principal is querying, updating, or being disclosed data from a forbidden property.

| Action  | Behavior                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| None    | No action is taken on the resource or data element.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| Audit   | The disclosure or update is permitted to continue, however a specialized security alert audit created indicating the property was disclosed or updated.                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| Redact  | <ul><li>On Resources with data policies, the resource is stripped of all information (identifiers, addresses, telecoms, etc.) and data is replaced with XXXXXX</li><li>On <code>AssigningAuthority</code> resource the value of the identifier is replaced with <code>XXXXXXX</code></li><li>On forbidden properties, the value of the property is replaced with <code>XXXXXX</code> on disclosure. Query is not permitted, recordation is not permitted.</li></ul><p>Note: The <code>$pep.masked</code> tag is appended to the resource.</p>                                                           |
| Nullify | <p>Replaces the value of the property with <code>null</code> , if the action is applied to a resource then the status is set to <code>Nullify</code> and no data is disclosed. <br>Note: The <code>$pep.masked</code> tag is appended to the resource.</p>                                                                                                                                                                                                                                                                                                                                              |
| Hide    | <ul><li>On Resources with data policies, the resource is removed from result sets. Direct fetching of the resource by UUID results in a <code>NotFound</code> and updates result in errors.</li><li>On <code>AssigningAuthority</code> resource, the identifier is removed from the object being disclosed. Updates or addition of the identity domain result in a privacy error.</li><li>On forbidden properties, the property is removed from the resource. Querying, recordation, and disclosure are forbidden. </li></ul><p>Note: The <code>$pep.masked</code> tag is appended to the resource.</p> |
| Error   | Whenever a principal attempts to read, query, or update the resource, the policy enforcement service will raise an error.                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| Hash    | <ul><li>On Resources with data policies, the resource has its properties replaced with the SHA256 hash of the value</li><li>On <code>AssigningAuthority</code> resource, the identifier is replaced with a hash of the identifier value.</li><li>On forbidden properties, this setting has no effect.</li></ul><p>Note: The <code>$pep.masked</code> tag is appended to the resource.</p>                                                                                                                                                                                                               |
