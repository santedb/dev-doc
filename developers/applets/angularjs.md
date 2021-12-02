---
description: >-
  This page provides information specifically related to AngularJS in SanteDB
  applets.
---

# AngularJS

SanteDB applets are written using the AngularJS framework. SanteDB's uicore (org.santedb.uicore) applet provides a series of useful Angular filters, directives and factories which can be used to write and compose user interfaces.

## Directives

There are a series of directives in the SanteDB AngularJS library which are used to render components.

### Entity Search (entity-search)

The entity-search directive is used to render a search box which can be used to search any SanteDB resource on the SanteDB API. This directive is used when you wish to provide simple searches to users. The structure of this directive is:

```markup
<entity-search
    type="[Patient|Person|Place|Organization|Act|AssigningAuthority|SecurityUser|..]"
    group-by="[Group Selector]"
    filter="[Filter Expression]"
  />  
```

For example, if you were to provide a search for all Places which are of type ServiceDeliveryLocation and grouped by their State the following entity-search could be used:

```markup
<entity-search
    type="Place"
    group-by="address.Direct.component.State"
    filter="{ &quot;classConcept.mnemonic&quot;:ServiceDeliveryLocation }"
/>
```

### Address Edit (address-edit)

The address editing control provides a common input control for `EntityAddress` types.&#x20;

```
<address-edit address="entity.address.HomeAddress"
    no-add="true|false"
    no-type="true|false"
    simple-entry="true|false"
    is-required="true|false"
    owner-form="name-of-form"
    control-prefix="'some-prefix'"/>
```

| Attribute      | Description                                                                                   |
| -------------- | --------------------------------------------------------------------------------------------- |
| address        | The `entity.address` field to bind to.                                                        |
| no-add         | When true, the user will not be permitted to add new types of this address to the entity.     |
| no-type        | When true, no type address (Home, Vacation, Work, etc.) will be shown.                        |
| simple-entry   | When true, a simplified version of the data entry form will be shown.                         |
| is-required    | When true, the address is required.                                                           |
| owner-form     | The name of the AngularJS form to which the address entry belongs.                            |
| control-prefix | When using multiple address entry forms on a single page, the prefix to add to each input id. |

#### Example of Use

```html
<div role="tabpanel" class="tab-pane fade" id="demoAddress">
    <address-edit owner-form="panel.editForm" address="editObject.address" is-required="true" />
</div>
```

### Name Edit (name-edit)

The name edit input control allows for the common reuse of a name entry component.

```
<name-edit
    name="name-to-bind-to"
    simple-name="true|false"
    no-add="true|false"
    no-type="true|false"
    simple-entry="true|false"
    is-required="true|false"
    owner-form="'name-of-form'"
    control-prefix="'prefix-to-add'" />
```

| Attribute      | Description                                                                                   |
| -------------- | --------------------------------------------------------------------------------------------- |
| name           | The `entity.name` field to bind to                                                            |
| no-add         | When true, the user will not be permitted to add new types of this name to the entity.        |
| no-type        | When true, no type name (legal, official, license, etc.) will be shown.                       |
| simple-name    | When true, the name input is shown as a single text box and names are not split into parts.   |
| simple-entry   | When true, a simplified version of the data entry form will be shown.                         |
| is-required    | When true, the address is required.                                                           |
| owner-form     | The name of the AngularJS form to which the address entry belongs.                            |
| control-prefix | When using multiple address entry forms on a single page, the prefix to add to each input id. |

### Demand (demand)

The demand directive is an attribute that can be attached to any button or link and is used to easily disable the link whenever the currently authenticated user does not have adequate permission to access the function.

```
<[button|a]
    demand="[Policy OID]"
>[text]</[button|a]>
```

For example, if you want to place a button on the page that will delete something important and wish to ensure that the user has been granted the "Unrestricted Administrative Function" policy (1.3.6.1.4.1.33349.3.1.5.9.2.0) you would use this syntax:

```
<button
    ng-click="deleteSomethingImportant()"
    demand="1.3.6.1.4.1.33349.3.1.5.9.2.0"
>{{ 'ui.myapp.deleteImportantThings' | i18n }}</button>
```

### Entity Table (entity-table)

The entity table is used to render a dynamic client side table which allows for filtering, sorting, and performing actions on lists (tables) of Entities. The entity table directive is used as follows:

```markup
<entity-table
    id="[id of table]"
    type="[SecurityUser|SecurityRole|Patient|Place|...]"
    search-field="[Property Path]"
    default-query="[Default Filter]"
    property-path="[Path To Display Property]"
    i18n-prefix="[Localization Prefix]"
    render="{ column: 'renderFunc' }"
    properties="[ column1, column2, ... ]"
    item-actions="[ { action settings } ]"
    actions="[ { table action settings } ]"
/>
```

The properties are described in more detail below:

| Attribute           | Description                                                                                                                                                                                                        |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| id                  | Uniquely identifies the entity table                                                                                                                                                                               |
| type                | Identifies the type name (resource name) which the table should be used to display                                                                                                                                 |
| search-field        | The field within the @type that is to be filtered when the user uses the search function of the table                                                                                                              |
| default-query       | The default HDSI query specification to use on the table (used to filter obsolete data)                                                                                                                            |
| property-path       | If the data you wish to display in the table is not at the root of the object, this is the path to select the display data.                                                                                        |
| i18n-prefix         | The localization prefix to be used when rendering buttons, column titles, etc. If you have a prefix of "org.myapp" then a column "userName" would be rendered with "org.myapp.userName"                            |
| render              | <p>Provides a series of rendering functions for the named columns. For example, to render "userName" using a function "renderUserName" the following value would be used:</p><p>{ userName: 'renderUserName' }</p> |
| properties          | A JavaScript array of properties from the object (root properties only) which are to be rendered.                                                                                                                  |
| can-filter          | When true, indicates the user can search the results in the entity table.                                                                                                                                          |
| external            | When true, binds the entity table to an upstream datasource.                                                                                                                                                       |
| can-sort            | When true, sorting is enabled.                                                                                                                                                                                     |
| stateless           | When true, a \_queryId parameter is not appended to queries that the entity-table does. This slows down pagination, however allows for dynamic refreshes of the data.                                              |
| sub-resource        | If querying from a sub-resource (example: `Patient/{id}/some-property` then the property to use.                                                                                                                   |
| sub-resource-holder | The UUID of the object which holds the sub-resource.                                                                                                                                                               |
| item-actions        | An array of objects which dictate which buttons to place on each column.                                                                                                                                           |
| actions             | An array of objects which dictate which buttons to place at the top of the table.                                                                                                                                  |

#### Rendering Buttons

Buttons are rendered on the entity-table using a series of control objects. Each control object is placed into an Array on either the item-actions or actions attributes in this format:

```javascript
{
    name: 'displayName',
    sref: 'ng-route state reference to use on button',
    action: 'javascript function to call on click',
    className: 'btn-* class to use on the button',
    icon: 'fa-* icon to use on button',
    demand: 'policy OID required to use button'
}
```

### Authority Select (authority-select)

The authority select directive creates a drop-down selection which allows a user to select an assigning authority based on a particular scope.&#x20;

```markup
<authority-select identity-scope="'bacd9c6f-3fa9-481e-9636-37457962804d'"
   key="[ property to extract key from ]" 
   ng-scope="[value]" />
```

| Attribute      | Description                                                                                                               |
| -------------- | ------------------------------------------------------------------------------------------------------------------------- |
| ng-scope       | The property/attribute where the value of the authority selection should be placed                                        |
| key            | The path on the objects returned from the server API where the "value" (what gets put into ng-scope) should be extracted. |
| identity-scope | The scope of the authorities to show in the selector (i.e. the types of authorities to show)                              |

### Concept Select (concept-select)

The concept select shows a searchable input which is bound to a concept set.

```
<concept-select 
    ng-scope="[value]"
    concept-set="'name-of-concept-set'"
    exclude-c        oncepts="[ 'uuid-of-concept-to-exclude' ]
    key="'path-to-key'"
/>
```

#### Parameters

| Attribute        | Type   | Description                                                                                                               |
| ---------------- | ------ | ------------------------------------------------------------------------------------------------------------------------- |
| ng-scope         | \*     | The property/attribute where the value of the selected concept selection should be placed                                 |
| key              | String | The path on the objects returned from the server API where the "value" (what gets put into ng-scope) should be extracted. |
| concept-set      | String | The name of the concept set to use to populate the searchable drop-down.                                                  |
| exclude-concepts | UUID   | The concepts to exclude from the selection box                                                                            |

#### Example Use

```
<concept-select class="form-control" required="required" concept-set="'PlaceClass'" ng-model="target.classConceptModel"/>
```

### Security Provenance (provenance)

The provenance filter is used to render the provenance data related to the object (create, update, or delete). Provenance is covered in more detail in architecture documentation. This filter renders in HTML so it should be bound as follows (the example shows the provenance for the user's creation data):

```markup
<div>
    <strong>Created:</strong>
    <provenance provenance-id="user.createdBy" provenance-time="user.creationTime"></provenance>
</div>
```

The output of this is a control which allows examination of the event including user, application, device, timestamp and session id.

![Rendering of the Provenance Filter](../../.gitbook/assets/image.png)

###

## Filters

SanteDB also provides a series of filters which are useful for rendering common objects. The filters are explained below.

### Localize (i18n)

The localize or i18n filter is used to automatically find the specified translation string in the global list of translations for the current locale. For example, to render string ui.action.save in the current locale:

```
{{ 'ui.action.save' | i18n }}
```

**Note:** One of the benefits of using SanteSuite's i18n filter rather than other AngularJS localization filters is that the server side will pre-process these tags and save the result of localization when deployed in production mode. This saves lower powered clients from re-running the filter on repeat views.

### Identifier (identifier)

The identifier filter is used to render the the specified identifier value from the specified domain (given a series of identifiers or a single identifier). For example, to render a patient's national health identifier:

```
{{ patient.identifier | identifier: 'NHID' }}
```

### Concept (concept)

The concept filter is used to render the preferred display name for a concept in the current locale. For example, to render the preferred display name of gender in the current locale:

```
{{ patient.genderConcept | concept }}
```

### Entity Name (name)

The name filter is used to render the specified type of name from the provided patient name collection. For example, to render a patient's legal name:

```
{{ patient.name | name: 'Legal' }}
```

### Entity Address (address)

The address filter, like the name filter, is used to render an entity's name. For example, to render the direct address of a place:

```
{{ place.address | address: 'Direct' }}
```

### Extended Date (ext-date)

The extended date (ext-date) filter is used to render dates according to the current user locale. This allows the developer to specify custom formats and custom precision. For example, the below code will show a patient's date of birth to the precision it was captured:

```
{{ patient.dateOfBirth | extDate: patient.dateOfBirthPrecision }}
```

