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
    display="'property.to.display'"
    search-field="'field-to-search-resources-on'"
    default-results="{ results to show by default }"
    filter="'hdsi expression'"
    group-display="'Group Display Selector'"
    group-by="[Group Selector]"
    key="'property path in ng-model to use as value'"
    selector="'property path to use as <option value='"
    value-property="path on scope to set selected value"
    value-selector="path on returned objects to set as selected value"
    multi-select="true|false"
    auto-tab-next="true|false"
    copy-nulls="true|false"
    min-render="10"
    change-clear="other object to watch - if its value changes then clear this"
    is-required="true|false"
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

```html
<address-edit address="address-to-update"
    no-add="true|false"
    no-type="true|false"
    simple-entry="true|false"
    is-required="true|false"
    owner-form="name-of-form"
    control-prefix="'some-prefix'"/>
```

| Attribute      | Type                                                                            | Description                                                                                   |
| -------------- | ------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- |
| address        | [EntityAddress](http://santesuite.org/assets/doc/js/santedb/EntityAddress.html) | The `entity.address` field to bind to. Note that ng-scope is not used on this directive.      |
| no-add         | Boolean                                                                         | When true, the user will not be permitted to add new types of this address to the entity.     |
| no-type        | Boolean                                                                         | When true, no type address (Home, Vacation, Work, etc.) will be shown.                        |
| simple-entry   | Boolean                                                                         | When true, a simplified version of the data entry form will be shown.                         |
| is-required    | Boolean                                                                         | When true, the address is required.                                                           |
| owner-form     | Form                                                                            | The name of the AngularJS form to which the address entry belongs.                            |
| control-prefix | String                                                                          | When using multiple address entry forms on a single page, the prefix to add to each input id. |

#### Example of Use

```html
<div role="tabpanel" class="tab-pane fade" id="demoAddress">
    <address-edit owner-form="panel.editForm" address="editObject.address" is-required="true" />
</div>
```

### Geographic Edit (geo-edit)

Allows for the editing of a geo-tag on an object.

```html
<geo-edit geo="entity.geo"
     is-required="true|false"
     owner-form="nameOfForm"
     control-prefix="'some-prefix'" />
```

| Attribute      | Type                                                              | Description                                                                               |
| -------------- | ----------------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| geo            | [GeoTag](http://santesuite.org/assets/doc/js/santedb/GeoTag.html) | The geographic tag which should be edited on this object (note that ng-scope is not used) |
| is-required    | Boolean                                                           | True if the information for the GEO tag must be entered.                                  |
| owner-form     | Form                                                              | The angular form which owns this input collection.                                        |
| control-prefix | String                                                            | The prefix to append to all inputs (for multiple geo-tag inputs)                          |

### Name Edit (name-edit)

The name edit input control allows for the common reuse of a name entry component.

```html
<name-edit
    name="name-to-bind-to"
    simple-entry="true|false"
    no-add="true|false"
    no-type="true|false"
    is-required="true|false"
    owner-form="'name-of-form'"
    input-style="tag|simple"
    allowed-components="prefix,given,family,suffix"
    control-prefix="'prefix-to-add'" />
```

| Attribute          | Type                                                                      | Description                                                                                      |
| ------------------ | ------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------ |
| name               | [EntityName](http://santesuite.org/assets/doc/js/santedb/EntityName.html) | The `entity.name` field to bind to                                                               |
| no-add             | Boolean                                                                   | When true, the user will not be permitted to add new types of this name to the entity.           |
| no-type            | Boolean                                                                   | When true, no type name (legal, official, license, etc.) will be shown.                          |
| simple-entry       | Boolean                                                                   | When true, a simplified version of the data entry form will be shown.                            |
| is-required        | Boolean                                                                   | When true, the address is required.                                                              |
| owner-form         | Form                                                                      | The name of the AngularJS form to which the address entry belongs.                               |
| control-prefix     | String                                                                    | When using multiple address entry forms on a single page, the prefix to add to each input id.    |
| input-style        | simple or tag                                                             | When `tag` is specified, each component of the name is a tag to split the name component values. |
| allowed-components | prefix, suffix, given, family                                             | A comma separated list of parts of the name which are permitted for entry.                       |

### Telecom Edit (telecom-edit)

The telecom editing control allows the UI to capture telecommunications addresses for an entity.

```html
<telecom-edit telecom="entity.telecom"
    single-edit="true|false"
    owner-form="true|false"
    no-label="true|false" />
```

### Identifier List Editor (identifier-list-edit)

The identifier list editing control allows the UI to capture identiifers on a key/value pair entry.

```html
<identifier-list-edit identifier="entity.identifier"
    owner-form="form that owns this control"
    container-class="entity.classConcept" />
```

### Identifier Edit (identifier-edit)

The identifier edit allows for the easy capture of a single identifier.

```html
<identifier-edit identifier="entity.identifier['SSN']"
    owner-form="name of owner form"
    container-class="entity.classConcept"
    no-domain="true|false"
    is-required="true|false"
    no-scan="true|false"
    no-label="true|false" />
```

### Relationship Edit (admin-relation-edit)

The relationship editor provides a generic entry for relationships to/from entities with one another.

```html
<admin-relation-edit 
    relationship="entity.relationship"
    container-class="entity.classConcept" />
```

### Schedule Editor (schedule-edit)

The schedule editor allows for editing of a [PlaceService ](http://santesuite.org/assets/doc/js/santedb/PlaceService.html)entry.

```
<schedule-edit
    json-schedule="json object | PlaceService.schedule" />
```

### Entity History (entity-history)

The entity history control allow for the display of a table outlining the history of an object.

```
<entity-history target="object_to_display_history" />
```

### Entity Policy Assignment (entity-policy-admin)

The policy assignment directive allows the UI to assign policies to any of the securable objects in SanteDB such as [SecurityDevice](http://santesuite.org/assets/doc/js/santedb/SecurityDevice.html), [SecurityRole](http://santesuite.org/assets/doc/js/santedb/SecurityRole.html), [SecurityApplication](http://santesuite.org/assets/doc/js/santedb/SecurityApplication.html), [Entity](http://santesuite.org/assets/doc/js/santedb/Entity.html), and [Act](http://santesuite.org/assets/doc/js/santedb/Act.html).

```
<entity-policy-admin securable="object-to-apply-policy-to"
    policy="collection of policy objects" />
```

### Demand (demand)

The demand directive is an attribute that can be attached to any button or link and is used to easily disable the link whenever the currently authenticated user does not have adequate permission to access the function.

```html
<[button|a]
    demand="[Policy OID]"
>[text]</[button|a]>
```

For example, if you want to place a button on the page that will delete something important and wish to ensure that the user has been granted the "Unrestricted Administrative Function" policy (1.3.6.1.4.1.33349.3.1.5.9.2.0) you would use this syntax:

```html
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
    type="SecurityUser|SecurityRole|Patient|Place|..."
    search-field="'field-to-search-on'"
    properties="[ 'list', 'of', 'properties', 'as', 'columns' ]"
    upstream="true|false"
    default-query="{ 'filter':value, 'filter': value }"
    item-actions="[{ name: 'button_name', 
        sref: 'nav-to-state', 
        action: 'callback',
        demand: 'required policy',
        className: 'button css class',
        icon: 'button icon',
        when: 'expression-when-to-show' 
    }]"
    actions="see item-actions"
    render="{ 'columnName' : 'renderingFunction' }",
    i18n-prefix="prefix-for-columns-in-translation"
    sort="true|false"
    default-filter="default search filter value"
    can-filter="true|false"
    can-size="true|false"
    no-buttons="true|false"
    button-bar="#refToButtonBarDiv"
    item-class="css class for items"
    stateless="true|false"
    sub-resource-holder="id-of-parent-resource"
    key-property="property of table key"
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
| upstream            | When true, binds the entity table to an upstream datasource.                                                                                                                                                       |
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

<table><thead><tr><th width="230.61443261852793">Attribute</th><th>Description</th></tr></thead><tbody><tr><td>ng-scope</td><td>The property/attribute where the value of the authority selection should be placed</td></tr><tr><td>key</td><td>The path on the objects returned from the server API where the "value" (what gets put into ng-scope) should be extracted.</td></tr><tr><td>identity-scope</td><td>The scope of the authorities to show in the selector (i.e. the types of authorities to show)</td></tr></tbody></table>

### Concept Select (concept-select)

The concept select shows a searchable input which is bound to a concept set.

```html
<concept-select 
    ng-scope="[value]"
    concept-set="'name-of-concept-set'"
    exclude-concepts="[ 'uuid-of-concept-to-exclude' ]"
    add-concept="[ 'uuid-of-extra-concepts' ]"
    key="'path-to-key'"
/>
```

#### Parameters

<table><thead><tr><th width="230.61443261852793">Attribute</th><th width="150">Type</th><th>Description</th></tr></thead><tbody><tr><td>ng-scope</td><td>*</td><td>The property/attribute where the value of the selected concept selection should be placed</td></tr><tr><td>key</td><td>String</td><td>The path on the objects returned from the server API where the "value" (what gets put into ng-scope) should be extracted.</td></tr><tr><td>concept-set</td><td>String</td><td>The name of the concept set to use to populate the searchable drop-down.</td></tr><tr><td>exclude-concepts</td><td>UUID[]</td><td>The concepts to exclude from the selection box</td></tr><tr><td>add-concept</td><td>UUID[]</td><td>Concepts which are to be added to the concept select (this is useful for adding null-flavor options)</td></tr></tbody></table>

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

![Rendering of the Provenance Filter](<../../../../.gitbook/assets/image (51) (1).png>)

###

### Entity List

{% hint style="info" %}
This feature is new to SanteDB 3.0
{% endhint %}

The `entity-list` directive behaves much like the `entity-table` only it presents a more mobile friendly view of results to the user. The `entity-list` can operate as a list, or as a grid of paged search results.

```html
<entity-list
    id="[id of list]"
    type="Person|SubstanceAdministration|Patient|Place|..."
    display="'list'|'grid'"
    search-field="'field-to-search-on'"
    upstream="true|false"
    default-query="{ 'filter':value, 'filter': value }"
    item-actions="[{ name: 'button_name', 
        sref: 'nav-to-state', 
        action: 'callback',
        demand: 'required policy',
        className: 'button css class',
        icon: 'button icon',
        when: 'expression-when-to-show' 
    }]"
    actions="see item-actions"
    item-supplement="function_to_call_for_each_record"
    order-by="sorting-order"
    can-filter="true|false"
    can-size="true|false"
    item-class="css class for items"
    stateless="true|false"
    sub-resource-scope="id-of-parent-resource"
    sub-resource="name_of_sub_resource"
    operation="name_of_operation"
    operation-scope="id-of-parent-resource"
    key-property="property of item key"
    >
    <!-- Template for each result card here -->
</entity-list>
```



<table><thead><tr><th width="186">Property</th><th width="159">Dynamic/Bind</th><th>Description</th></tr></thead><tbody><tr><td>id</td><td>No</td><td>The unique identifier for the DOM element representing the root of the item list.</td></tr><tr><td>type</td><td>No</td><td>The name of the resource which is used to populate the table.</td></tr><tr><td>display</td><td>Yes</td><td>The display of the list either <code>grid</code> for a grid of results or <code>list</code> for a simple list.</td></tr><tr><td>search-field</td><td>Yes</td><td>The field which is used to search for objects in <code>@type</code></td></tr><tr><td>upstream</td><td>Yes</td><td>True if the search should be executed against the upstream server or false for a local search.</td></tr><tr><td>default-query</td><td>Yes</td><td>The query which is used to filter the initial set of results.</td></tr><tr><td>item-actions</td><td>Yes</td><td>The actions which should be placed in the footer of each result.</td></tr><tr><td>actions</td><td>Yes</td><td>The actions which should be placed in the header of the the result.</td></tr><tr><td>item-supplement</td><td>Yes</td><td>The function which should be called for each result. These functions can fetch additional data or make computations for the view model for each result.</td></tr><tr><td>order-by</td><td>No</td><td>The default sorting expression for results in the format : <code>field_name:[asc|desc]</code></td></tr><tr><td>can-filter</td><td>No</td><td>When explicitly set to false the filtering option will not appear</td></tr><tr><td>can-size</td><td>No</td><td>When set to true, allow the user to select the number of results.</td></tr><tr><td>item-class</td><td>No</td><td>The CSS class which should be applied to every result.</td></tr><tr><td>stateless</td><td>No</td><td>When set to true, indicates that each pagination of search of the resource should not include <code>_queryId</code></td></tr><tr><td>sub-resource-scope</td><td>Yes</td><td>The id in which the <code>@sub-resource</code> path is applied.</td></tr><tr><td>sub-resource</td><td>No</td><td>The name of the sub-property/resource on the API to query</td></tr><tr><td>operation-scope</td><td>Yes</td><td>The id in which the <code>@operation</code> path is applied</td></tr><tr><td>operation</td><td>No</td><td>The name of the operation to invoke to query for results</td></tr><tr><td>key-property</td><td>No</td><td>The name of the property which serves as the KEY for the result</td></tr></tbody></table>

For example, to display all `Place` in a grid of results:

```html
<entity-list type="Place" display="'grid'" search-field="'name.component.value'" 
   item-actions="[
      {
         name: 'view',
         sref: 'santedb-admin.data.place.view',
         className: 'btn-primary',
         icon: 'fa-eye'
   ]">
   <div class="card-header">
       <h5 class="card-title">{{ item.name | name }}</h5>
    </div>
 </entity-list>
```

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

