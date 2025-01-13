# Facility Administration

{% hint style="info" %}
This page documents a SanteDB 3.0 Feature
{% endhint %}

In SanteDB a [Place](../../../../santedb/data-and-information-architecture/conceptual-data-model/entities/data-dictionary.md#place)  is a specialized entity used to represent a physical place. SanteDB further distinguishes between classifications of places in Service Delivery Locations (Facilities) and geographic places.&#x20;

The term **Facility** is used to describe Service Delivery Locations, or places that deliver services.&#x20;

## Facility Hierarchy

Facilities exist in a hierarchy much like Places edited through the Place hierarchy. This facility hierarchy is used for several functions including:

* Automatically routing requests for supply from the parent to children
* Reporting roll-up by medical area/division/national hospitals

## Facility List

Opening the **Reference Data > Facilities** view brings up the master facility listing in the CDR. This screen allows adminsitrators to:

* Search for existing facilities in their CDR instance
* Create a new facility
* Export the facility list to a dataset to be imported onto another SanteDB server
* Delete facilities from the CDR

<figure><img src="../../../../.gitbook/assets/image (530).png" alt=""><figcaption></figcaption></figure>

## Creating a Facility

Before creating a new facility, administrators should:

* Understand where in the hierarchy the facility lay
* Understand the purpose of the facility (stock distribution, care delivery, etc.)
* Have details about facility location including:
  * Physical Address&#x20;
  * Global Location Number (GLN)
  * Contact information

The create facility screen is accessed using the **Create** button on the facility list. Administrators will be prompted to enter basic information about the facility.

<figure><img src="../../../../.gitbook/assets/image (531).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
If the facility has a known geographic location, clicking the **Known Geolocation** will allow for the entry of latitude and longitude values. Mobile facilities are those which have no fixed address, such as a hospital ship, or traveling vaccination clinic.
{% endhint %}

## Facility Details

The facility detail screen allows for:

* Editing the base level facility details (identification, name, contact details, etc.)
* Editing the services and schedules for those services&#x20;
* Editing/viewing the place hierarchy
* Editing/changing the place catchment/service areas
* Assigning staff and managers

<figure><img src="../../../../.gitbook/assets/image (532).png" alt=""><figcaption></figcaption></figure>

### Facility Profile

The facility profile tab allows administrators to change the core facility details for the place which is being edited. &#x20;

<figure><img src="../../../../.gitbook/assets/image (533).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
In order to use the GS1 BMS XML interface, administrators are encouraged to enter the Global Location Number (GLN) for the facilities in order to facilitate order flows.
{% endhint %}

### Facility Services

The SanteDB CDR can provide search functions related to finding faciliites which offer particular services. In order to use this functionality, one or more services should be added to the facility with an optional schedule.

<figure><img src="../../../../.gitbook/assets/image (534).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
In SanteEMR - non-administrative users who are assigned as Managers of the clinic are permitted to make changes to the facility service schedules.
{% endhint %}

### Facility Service Areas

Service areas allow an administrator to configure catchment information for a facility. These service areas are places (cities, towns, villages, regions, etc.) where patients residing in those areas can be assigned.

<figure><img src="../../../../.gitbook/assets/image (535).png" alt=""><figcaption></figcaption></figure>

To assign a service area to a facility, enter the name o fthe place which is to be assigned and press the **Add** button.

### Staffing

Some deployments of SanteDB have the security policy `allowNonAssignedUsers` set to false. This means that users which are not assigned to that facility, will not have the ability to login to those devices, nor select that they are operating on behalf of that facility.&#x20;

This information is controlled on the **Staffing** tab of the Facility.

<figure><img src="../../../../.gitbook/assets/image (536).png" alt=""><figcaption></figcaption></figure>

To assign staff to a facility, search for the user's name and press the **Assign** button.&#x20;

To assign an existing member of staff as a manager, press the **Manager** button on their staff assignment. Managers are permitted to:

* Alter service schedules for the facility which they manage
* Perform stock counts, adjustments, etc.
* Start sessions for other users and clinics which are children of the facility they manage

Managers of clinics are not (by default) local administrators of that clinic. Rather, these types of users must be assigned as a clinic manager and also a local adminsitrator.

### Stock Stores

{% hint style="info" %}
This feature is only enabled on installations of SanteIMS EIR 3.0
{% endhint %}

When the SanteIMS EIR plugins are installed and active on your SanteDB installation, the facility page will provide an extra tab for stock management at the facility. Stock stores are used by SanteIMS to manage the places within a facility where stock is physically kept. Stock stores include:

* Refrigerators for vaccinations and cold-chain stock items
* Freezers for deep-cold vaccinations (such as mRNA SARS nCOV-2)
* Pantries for non-cold store stock (syringes, vitamins, etc.)

Stock stores are managed on the stock tab.

<figure><img src="../../../../.gitbook/assets/image (9) (1).png" alt=""><figcaption></figcaption></figure>

Using this summary view, administrators may:

* Create a new stock store within the facility
* Remove stock stores from the facility
* View current contents of the stock store (lots and quantities) as well as a history of previous stock counts performed by the facility
* View current and historical functional status and temperature readings for the facility
* Initiate an administrative stock count or stock take
* Initiate an administrative temperature reading / functional status report

#### Creating a Stock Store

To create a new stock store, the administrator should use the **Create** option, this will allow the administrator to enter the details about the new store:

<figure><img src="../../../../.gitbook/assets/image (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

The fields for the stock containers are:

* **Name/Description:** A friendly name for the fridge that is shown to users when they perform stock counts or temperature readings.
* **Type:** The type of stock store such as a cold store (Fridge, Freezer, Cold Box/Flask) or a regular store (Pantry, Box, etc.)
* **Identifiers:** One or more identifiers which are scoped to **Container** which are used to uniquely identify the fridge
* **Manufacturer:** If the stock store is a manufactured container (such as a fridge or freezer) which may require repair and/or service, this indicates the manufacturer of the store.
* **Serial #**: If a serial or model number is required for service, this is the serial number of the unit
* **Expires:** Some cold storage units have expiration dates or dates where their certification period ends.&#x20;
* **Max Capacity:** The maximum capacity (policy) of the store.
