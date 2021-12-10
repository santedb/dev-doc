# JavaScript API

SanteDB provides a JavaScript based API which can be used with the default AngularJS UI components, or can be called from other, third party UI frameworks. The core SanteDB API is contained in the applet `org.santedb.core` , and are called from the SanteDB object.

## Reference Documentation

The SanteDB JavaScript API is documented using JSDoc, this resource is available at the [JavaScript API Documentation](http://santesuite.org/assets/doc/js/santedb/) site, however also appear within the code completion within Visual Studio Code.

In order to import the documentation for VS Code, you should reference the core API files santedb.js and santedb-model.js from VS Code (usually these files are available in the .ref/ folder).

```javascript
/// <reference path="../../.ref/js/santedb.js"/>
/// <reference path="../../.ref/js/santedb-model.js"/>
angular.module('santedb').controller('MyController', ["$scope", "$rootScope", function ($scope, $rootScope) {

}]);
```

Once this reference is included in your file you should see documentation from the source files in VS Code.

![](<../../../../.gitbook/assets/image (162).png>)

## Core API

The core API is accessed using the SanteDB object within your JavaScript project. The main SanteDB API has three properties which, themselves, are utilities for accessing the API. The helper classes in the SanteDB object are:

| Property / Utility | Description                                                                                                           |
| ------------------ | --------------------------------------------------------------------------------------------------------------------- |
| resources          | Used for search, updating, deleting, etc. resources on the API                                                        |
| configuration      | Used for retrieving / saving configuration data                                                                       |
| application        | Used for interacting with the DCG application such as fetching installed applets, version information, restarts, etc. |
| locale             | Localization services including string translations and changing the current locale of the UI.                        |
| authentication     | Tools for establishing a session, overriding the current session, etc.                                                |

### Resource Interaction

The HDSI and AMI resources have been wrapped into convenient helper utilities in the SanteDB.resources property. Below is an example of using these resources to search for and update a patient.

```javascript
try {
    /** @type {Patient} */
    var patient = await SanteDB.resources.patient.getAsync($state.patientId);
    if(patient.statusConcept == StatusKeys.New) {
        patient.statusConcept = StatusKeys.Active;
        patient.tag["$reviewed"] = "true";
        patient = await SanteDB.resources.patient.updateAsync(patient.id, patient);
    }
}
catch(e) {
    $rootScope.errorHandler(e);
}
```

All resources in the `SanteDB.resources` utility expose the following methods

| Method                | Return             | Description                                                                                                                                                       |
| --------------------- | ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| getAsync              | Resource           | Retrieve a specific instance of a resource by its UUID                                                                                                            |
| findAsync             | Bundle             | Execute an [HDSI Query ](../../../service-apis/hl7-fhir/hdsi-query-syntax.md)against the resource returning a bundle of results.                                  |
| insertAsync           | Inserted Resource  | Insert a new instance of the resource on the API.                                                                                                                 |
| updateAsync           | Updated Resource   | Update an existing instance of the resource                                                                                                                       |
| deleteAsync           | Deleted Resource   | Delete a resource by its UUID.                                                                                                                                    |
| cancelAsync           | Cancelled Resource | Cancel the resource by its UUID (note: this method is only supported for Acts)                                                                                    |
| nullifyAsync          | Nullified Resource | Nullify the specified resource (i.e. the resource never existed)                                                                                                  |
| patchAsync            | Patched Resource   | Submit a patch against the specified resource type and instance. Patches are constructed using [the patch format.](../../../service-apis/gs1-bms-xml/patching.md) |
| lockAsync             | Resource           | Locks the specified resource (if supported by the resource), forbidding action on that resource.                                                                  |
| unlockAsync           | Resource           | Unlocks the specified resource (if supported by the resource)                                                                                                     |
| addAssociatedAsync    | Resource           | Add an associated object to the root resource. For example, add role X to user Y.                                                                                 |
| getAssociatedAsync    | Resource           | Get a specific instance of an associated resource.                                                                                                                |
| findAssociatedAsync   | Bundle             | Find the associated resource instances (i.e. find associated roles for user X)                                                                                    |
| removeAssociatedAsync | Resource           | Remove an associated resource from an instance.                                                                                                                   |
