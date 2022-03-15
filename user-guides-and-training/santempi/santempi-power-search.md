# SanteMPI Power Search

The SanteMPI power search allows power users to perform in-depth searches of the SanteMPI's underlying CDR using the [hdsi-query-syntax](../../developers/service-apis/health-data-service-interface-hdsi/hdsi-query-syntax/ "mention"). This allows data administrators to find specific records based on any criteria which is stored in the SanteMPI database.

{% hint style="info" %}
Some SanteMPI servers impose minimum search criteria and/or restricted search criteria on their databases. Depending on the data privacy configuration of the deployed software and the user's access level, certain fields may be restricted.
{% endhint %}

When a user visits the power search screen, they are presented with an empty search input area.

![](<../../.gitbook/assets/image (448) (1) (1) (1) (1).png>)

## Creating Search Criteria

To begin, enter the HDSI query expression clause. The software will provide suggestions for property clause paths which match the Patient resource. Users can select the property they wish to filter on.

![](<../../.gitbook/assets/image (449) (1) (1) (1) (1).png>)

Users may use keyboard shortcuts to navigate the suggestions:

* Up / Down - Select the previous or next suggestion
* Tab - Auto-fill the selected suggestion

Depending on the search type of the current path, the user should select the appropriate operator for the search clause.&#x20;

| `equal`                 | The value in the database at the property path must exactly match the value specified | All Types                    |
| ----------------------- | ------------------------------------------------------------------------------------- | ---------------------------- |
| `not-equal`             | The value in the database must not match the value specified                          | All Types                    |
| `less-than`             | The value in the database must be less than the value provided.                       | `DateTime`, `Int32`, `Int64` |
| `less-than-or-equal`    | The value in the database must be less than or equal to the value provided            | `DateTime`, `Int32`, `Int64` |
| `greater-than`          | The value in the database must be greater than the value provided                     | `DateTime`, `Int32`, `Int64` |
| `greater-than-or-equal` | The value in the database must be greater than or equal to the value specified.       | `DateTime`, `Int32`, `Int64` |
| `approx`                | The value must match the pattern of the value provided                                | `String`                     |

### Repeat Clauses

Multiple repetitions of the same HDSI path result in logic as described below.

| `less-than`, `less-than-equal`, `greater-than`, `greater-than-equal` | <ul><li>LOGICAL OR when same operator applied</li><li>LOGICAL AND when different operators applied</li></ul> |
| -------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| `not-equal`                                                          | <ul><li>LOGICAL AND</li></ul>                                                                                |
| `equal`, `approx`                                                    | <ul><li>LOGICAL OR</li></ul>                                                                                 |

For example, the following expression results in patients who were born between `1980-01-01` and `1980-12-31`

![](<../../.gitbook/assets/image (438) (1) (1) (1) (1).png>)

Conversely, the following expression results in patients named Donny or Don

![](<../../.gitbook/assets/image (440) (1) (1) (1) (1).png>)

### Concept Fields

Whenever the HDSI expression is a filter on a property of type `Concept` the value will be a search, of concepts.

![](<../../.gitbook/assets/image (430) (1) (1) (1).png>)

### Entity Fields

Whenever the HDSI expression is a filter on a property of type `Entity` or when of its derivatives, the search box will be a drop down of entities. For example, searching by citizen results in a search of entities (since `.target` is bound to Entity) .

![](<../../.gitbook/assets/image (429) (1) (1) (1).png>)

Using the cast operator `@` the input can be filtered to places only.

![](<../../.gitbook/assets/image (431) (1) (1).png>)

### Deep Linking Queries

If the SanteDB instance is collecting data other than patient registrations (such as vaccinations), the properties of patient can be linked deeply. For example, if we wanted to filter on patients who have received a vaccination of a particular product.

![](<../../.gitbook/assets/image (441) (1) (1) (1) (1) (1) (1).png>)

## Related Topics

{% content-ref url="santempi-searching.md" %}
[santempi-searching.md](santempi-searching.md)
{% endcontent-ref %}

{% content-ref url="the-patient-dashboard/" %}
[the-patient-dashboard](the-patient-dashboard/)
{% endcontent-ref %}
