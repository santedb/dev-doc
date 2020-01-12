---
description: >-
  This page provides information specifically related to AngularJS in SanteDB
  applets.
---

# AngularJS

SanteDB applets are written using the AngularJS framework. SanteDB's uicore \(org.santedb.uicore\) applet provides a series of useful Angular filters, directives and factories which can be used to write and compose user interfaces.

## Directives

There are a series of directives in the SanteDB AngularJS library which are used to render components.

### Entity Search \(entity-search\)

The entity-search directive is used to render a search box which can be used to search any SanteDB resource on the SanteDB API. This directive is used when you wish to provide simple searches to users. The structure of this directive is:

```text
<entity-search
    type="[Patient|Person|Place|Organization|Act|AssigningAuthority|SecurityUser|..]"
    group-by="[Group Selector]"
    filter="[Filter Expression]"
  />  
```

For example, if you were to provide a search for all Places which are of type ServiceDeliveryLocation and grouped by their State the following entity-search could be used:

```text
<entity-search
    type="Place"
    group-by="address.Direct.component.State"
    filter="{ &quot;classConcept.mnemonic&quot;:ServiceDeliveryLocation }"
/>
```

### Demand \(demand\)

The demand directive is an attribute that can be attached to any button or link and is used to easily disable the link whenever the currently authenticated user does not have adequate permission to access the function.

```text
<[button|a]
    demand="[Policy OID]"
>[text]</[button|a]>
```

For example, if you want to place a button on the page that will delete something important and wish to ensure that the user has been granted the "Unrestricted Administrative Function" policy \(1.3.6.1.4.1.33349.3.1.5.9.2.0\) you would use this syntax:

```text
<button
    ng-click="deleteSomethingImportant()"
    demand="1.3.6.1.4.1.33349.3.1.5.9.2.0"
>{{ 'ui.myapp.deleteImportantThings' | i18n }}</button>
```

### Entity Table \(entity-table\)

The entity table is used to render a dynamic client side table which allows for filtering, sorting, and performing actions on lists \(tables\) of Entities. The entity table directive is used as follows:

```text
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

<table>
  <thead>
    <tr>
      <th style="text-align:left">Attribute</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">id</td>
      <td style="text-align:left">Uniquely identifies the entity table</td>
    </tr>
    <tr>
      <td style="text-align:left">type</td>
      <td style="text-align:left">Identifies the type name (resource name) which the table should be used
        to display</td>
    </tr>
    <tr>
      <td style="text-align:left">search-field</td>
      <td style="text-align:left">The field within the @type that is to be filtered when the user uses the
        search function of the table</td>
    </tr>
    <tr>
      <td style="text-align:left">default-query</td>
      <td style="text-align:left">The default HDSI query specification to use on the table (used to filter
        obsolete data)</td>
    </tr>
    <tr>
      <td style="text-align:left">property-path</td>
      <td style="text-align:left">If the data you wish to display in the table is not at the root of the
        object, this is the path to select the display data.</td>
    </tr>
    <tr>
      <td style="text-align:left">i18n-prefix</td>
      <td style="text-align:left">The localization prefix to be used when rendering buttons, column titles,
        etc. If you have a prefix of &quot;org.myapp&quot; then a column &quot;userName&quot;
        would be rendered with &quot;org.myapp.userName&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left">render</td>
      <td style="text-align:left">
        <p>Provides a series of rendering functions for the named columns. For example,
          to render &quot;userName&quot; using a function &quot;renderUserName&quot;
          the following value would be used:</p>
        <p>{ userName: &apos;renderUserName&apos; }</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">properties</td>
      <td style="text-align:left">A JavaScript array of properties from the object (root properties only)
        which are to be rendered.</td>
    </tr>
    <tr>
      <td style="text-align:left">item-actions</td>
      <td style="text-align:left">An array of objects which dictate which buttons to place on each column.</td>
    </tr>
    <tr>
      <td style="text-align:left">actions</td>
      <td style="text-align:left">An array of objects which dictate which buttons to place at the top of
        the table.</td>
    </tr>
  </tbody>
</table>#### Rendering Buttons

Buttons are rendered on the entity-table using a series of control objects. Each control object is placed into an Array on either the item-actions or actions attributes in this format:

```text
{
    name: 'displayName',
    sref: 'ng-route state reference to use on button',
    action: 'javascript function to call on click',
    className: 'btn-* class to use on the button',
    icon: 'fa-* icon to use on button',
    demand: 'policy OID required to use button'
}
```

## Filters

SanteDB also provides a series of filters which are useful for rendering common objects. The filters are explained below.

### Localize \(i18n\)

The localize or i18n filter is used to automatically find the specified translation string in the global list of translations for the current locale. For example, to render string ui.action.save in the current locale:

```text
{{ 'ui.action.save' | i18n }}
```

**Note:** One of the benefits of using SanteSuite's i18n filter rather than other AngularJS localization filters is that the server side will pre-process these tags and save the result of localization when deployed in production mode. This saves lower powered clients from re-running the filter on repeat views.

### Identifier \(identifier\)

The identifier filter is used to render the the specified identifier value from the specified domain \(given a series of identifiers or a single identifier\). For example, to render a patient's national health identifier:

```text
{{ patient.identifier | identifier: 'NHID' }}
```

### Concept \(concept\)

The concept filter is used to render the preferred display name for a concept in the current locale. For example, to render the preferred display name of gender in the current locale:

```text
{{ patient.genderConcept | concept }}
```

### Entity Name \(name\)

The name filter is used to render the specified type of name from the provided patient name collection. For example, to render a patient's legal name:

```text
{{ patient.name | name: 'Legal' }}
```

### Entity Address \(address\)

The address filter, like the name filter, is used to render an entity's name. For example, to render the direct address of a place:

```text
{{ place.address | address: 'Direct' }}
```

### Security Provenance \(provenance\)

The provenance filter is used to render the provenance data related to the object \(create, update, or delete\). Provenance is covered in more detail in architecture documentation. This filter renders in HTML so it should be bound as follows \(the example shows the provenance for the user's creation data\):

```markup
<div>
    <strong>Created:</strong>
    <span ng-bind-html="user.createdBy | provenance: user.creationTime"></span>
</div>
```

The output of this is a control which allows examination of the event including user, application, device, timestamp and session id.

![Rendering of the Provenance Filter](../../../.gitbook/assets/image%20%2824%29.png)

### Extended Date \(ext-date\)

The extended date \(ext-date\) filter is used to render dates according to the current user locale. This allows the developer to specify custom formats and custom precision. For example, the below code will show a patient's date of birth to the precision it was captured:

```text
{{ patient.dateOfBirth | extDate: patient.dateOfBirthPrecision }}
```



