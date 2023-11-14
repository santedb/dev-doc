# Place Administration

{% hint style="info" %}
This help page requires version 3.0 of SanteDB
{% endhint %}

In SanteDB a [Place](../../../../santedb/data-and-information-architecture/conceptual-data-model/entities/data-dictionary.md#place)  is a specialized entity used to represent a physical place. SanteDB further distinguishes between classifications of places in Service Delivery Locations (Facilities) and geographic places.&#x20;

The Place administration screen is used to edit non-service delivery locations and is used to express the geographical hierarchy within a SanteDB instance. This can be villages, provinces, cities, and countries. SanteDB uses these entries in a variety of manners:

* If fully structured address inputs are enabled, SanteDB uses these Place registrations to populate the drop-downs based on hierarchy of previous inputs.
* Catchment assignment with facilities (and by extension, the assignment of a Patient to a default home facility based on catchment)
* Subscriptions when basing subscriptions off geographic areas of data

## Place Hierarchy

Places in SanteDB can be established in a hierarchy using the place editing screen. The place editing process allows the linkages of places in a Parent/Child relationship. To illustrate this using Ontario Canada as an example:

<figure><img src="../../../../.gitbook/assets/image (51).png" alt=""><figcaption></figcaption></figure>

The example, would consist of 4 places in the SanteDB database:

1. A place named "Canada" with a classification of Country at the root (with no parent)
2. A place named "Ontario" with a classification of State or Province, with a parent of Canada (#1) and two children of Toronto (#3) and Ottawa (#4)
3. A place named "Toronto" with a classification of City or Town and a parent of Ontario (#2)
4. A place named "Ottawa" with a classification of City or Town and a parent of Ontario (#2)

## Place List

The master place list is accessed via the **Reference Data > Places** menu item. Upon visiting the place screen, users will be presented with a list of all the places which have been registered in the SanteDB solution which are not service delivery locations.

<figure><img src="../../../../.gitbook/assets/image (64).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
SanteDB contains place registrations for countries - when implementing a place hierarchy it is recommended that implementers bind the top level of their hierarchy (typically provinces or states) to the SanteDB registered country.
{% endhint %}

## Creating a Place

To create a place press the **Create** button, this will present the administrator with a basic entry form to enter the key details about new place:

<figure><img src="../../../../.gitbook/assets/image (7) (2).png" alt=""><figcaption></figcaption></figure>

The form fields to be provided are:

| Field          | Description                                                                                                                                                          | Example           |
| -------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------- |
| Classification | The standard classification of the geographic place in SanteDB. See [SanteDB Place Hierarchy](place-administration.md#santedb-place-hierarchy) for more information. | State or Province |
| Type           | The sub-classification/custom classification of the geographic place. This can be used for customizing your own place hierarchy or specifying a sub-specialization.  | Union Territory   |
| Official Name  | The official name for the place as it should appear in drop downs, reports, etc.                                                                                     | Capitolville      |
| Parent         | If the place is a child of another place (such as a province is a specialization of country)                                                                         | SampleCountry     |

### SanteDB Place Hierarchy & Classifications

In order for drop downs in the SanteDB user interface to be cascaded according to hierarchy, all geographic places must have a classification assigned to them in the standardized hierarchy. By using standardized hierarchies, developers can understand your own custom administrative structure with SanteDB's. The standardized classifications in order:

* Country: Represents the top of the geographic hierarchy.
* Nation: Represents a geographical grouping of people based on culture, language, ethnic background, etc. (for example: Sioux Nation as a child of Canada)
* State or Province: A sub-national subdivision of a country such as a territory, state, province, region, etc.
* County or Parish: A sub-provincial subdivision of a province or state which is used for administrative oversight (county boards, or governing councils, etc.).&#x20;
* City or Town: An incorporated or recognized area of land with a municipal governance structure.

SanteDB also includes a generic **Place** classification which should be used when a classification of a place does not apply (such as an ungoverned island, an orbiting space station, other planets, etc.)

## Place Details

After creating a place, or viewing a place from the existing list of places registered in the SanteDB service, the Administrator will be presented with the place details screen illustrating the hierarchy, the facilities which service this area (facilities where the place is in catchment) and the relationships the place carries.

<figure><img src="../../../../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

### Changing Status

To change the place status, administrators should click on the status indicator and select another state to place the Place instance into:

<figure><img src="../../../../.gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure>

Statuses here follow the normal [Entity State Machine](../../../../santedb/data-and-information-architecture/conceptual-data-model/entities/state-machine.md).

### Editing Core Properties

The core properties can be edited by clicking the pencil icon in the **Place Properties** panel. This will switch the editing panel into edit mode:

<figure><img src="../../../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Changing the Classification of the place is only recommended if the place does not have any active relationships. Modification of the classification may invalidate some relationships and may cause issues for any existing data.
{% endhint %}

#### Adding Aliases

In many contexts, places may have additional pseudonyms which can be used to reference places. For example, the city Hamilton/Wentworth may also be referred to by local residents as just Hamilton, or Stoney Creek. All these names should point to the official registration for Hamilton/Wentworth.

The Name tab on the edit screen can be used to modify these aliases and can be used to add other names to the place:

<figure><img src="../../../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

#### Adding Identifiers

Geographical places may carry official identifiers which are referenced in addresses or other systems (for example, all countries in SanteDB carry an ISO-3166 identifier). The **Identifiers** tab should be used to associate identifiers with the place. To add an identifier:

1. Select the assigning authority&#x20;
2. Enter the ID number&#x20;
3. Press the **+** button to add the identifier to the list

<figure><img src="../../../../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

Identifiers can be removed using the **X** button beside the identifier to be removed.&#x20;

<figure><img src="../../../../.gitbook/assets/image (58).png" alt=""><figcaption></figcaption></figure>

#### Adding Addresses

The address on a place (City, Province, Country, etc.) often serves the address template whenever a structure address is selected for this place. Addresses should be updated whenever the parent relationship changes, or can be used to specify the address template for objects created within this place.

<figure><img src="../../../../.gitbook/assets/image (9) (2).png" alt=""><figcaption></figcaption></figure>

### Editing Hierarchy

The place hierarchy is used to establish the parent and children of the geographic place within the SanteDB system. The hierarchy is listed in the Hierarchy panel on the place details screen.

<figure><img src="../../../../.gitbook/assets/image (1) (3).png" alt=""><figcaption></figcaption></figure>

Child places can be removed directly from the hierarchy window without entering edit mode. However, if the parent or new children are to be added, the administrator must click on the Pencil icon to enter edit mode which will enable the form inputs.

Adding a child link requires searching for the child place to add and pressing the **Add** button.

<figure><img src="../../../../.gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
A place can have only one Parent. When changing the parent of the current place or when changing the parent by associating a child, you will be prompted to confirm the action. Changing the place hierarchy may require editing other data such as addresses.
{% endhint %}

### Adding Service Facilities

SanteDB supports the assignment of dedicate service delivery locations (facilities) which service the geographic region. This can be performed via the facility editing screen, or can be performed directly in the Place editing screen. Assigning a facility starts with pressing the **Add** button on the **Service Facilities** panel.

<figure><img src="../../../../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

### Associating an Existing Facility

The default option when adding a dedicated service delivery location is to link an existing facility. This is done by searching for an existing facility and pressing ADD.

<figure><img src="../../../../.gitbook/assets/image (6) (2).png" alt=""><figcaption></figcaption></figure>

### Associating a New Facility

Alternately, an administrator can create a new facility selecting **Associate a New Facility**.&#x20;

&#x20;

<figure><img src="../../../../.gitbook/assets/image (3) (2).png" alt=""><figcaption></figcaption></figure>

The administrator should complete the minimum fields, select the additional data elements (if known) and then press the ADD button.

