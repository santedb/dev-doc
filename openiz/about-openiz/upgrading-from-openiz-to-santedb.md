# Upgrading from OpenIZ to SanteDB

SanteDB has many features which make it a desirable upgrade from the 1.x version of OpenIZ. Some key features of SanteDB over OpenIZ:

* Uses OpenID Connect to allow for SSO infrastructure
* Allows for guards on Business Rules to reduce JavaScript function calls for business rules
* Allows higher granularity of security controls \(policy on entities and identifier domains\)
* Has unified runtime environment \(no more writing one offs between web and mobile\)
* Has more robust audit logging and conflict resolution measures
* Supports MDM and classic single instance mode
* Much more.

### Upgrading your Database

Upgrading the database is a matter of running the 00OIZ\_UPGRADE.SQL script against your OpenIZ database, the process for this is:

1. Make a backup of your current database
2. Open your favorite PostgreSQL client
3. Run the 00OIZ\_UPGRADE SQL file
4. Apply the relevant patches to your database \(found in the GitHub, usually the 2019\* and 2020\* patch files for PostgreSQL are required\)

#### Key Data Schema Changes

The major changes for the database are:

* Migration to store security modification attributes \(created, update, obsolete\) as provenance objects tracking user/app/device/session which made the change.
* Addition of Finance entities into the persistence layer
* Switching automatic UUID generation from v4 \(random\) to v1 \(time-based\) to better allow indexes to perform \(note: upgrade does not re-key any data\)

### Upgrading the Integrations

Upgrading your integrations will depend on the interfaces you're using. If you're using one of the following interfaces:

* HL7 Version 2.x
* GS1 BMS XML
* HL7 FHIR

You should not require any additional work to upgrade these interfaces as they remain unchanged. If you're using one of the following interfaces:

* AMI

You will only need to change the XML Namespace from http://openiz.org to http://santedb.org. If you're using one of the following interfaces, your upgrade will be more complex:

* IMSI -&gt; Has been refactored to the HDSI with namespace change and resource organization \(see OpenAPI documentation\). Level of effort of upgrading these integrations will be moderate.
* RISI -&gt; Has been obsoleted. The RISI still exists in SanteDB however is not undergoing active development or testing, so it is entirely possible it won't work. \(If you'd like to maintain the RISI join our community\). Instead the RISI has been moved:
  * Ad-Hoc Query Interface -&gt; See the BIS
  * Reports Interface -&gt; No equivalent in SanteDB

### Upgrading User Interface

The user interface is perhaps the largest effort upgrading from OpenIZ to SanteDB. 

#### New API Pattern

As an illustration in the difference of API patterns, below is the code used in OpenIZ to retrieve an alert \(a mail message in SanteDB\):

```javascript
OpenIZ.App.getAlertsAsync({
    query: {
        id: $stateParams.alertId,
        _count: 1
    },
    onException: function (ex)
    {
        OpenIZ.App.hideWait();

        if (typeof (ex) == "string")
            console.log(ex);
        else if (ex.message != undefined)
            console.log("" + ex.message + " - " + ex.details);
        else
            console.log(ex);
    },
    continueWith: function (data)
    {
        $scope.alert = data[0];
        $scope.alert.body = $scope.alert.body.replace("\n", "<br/>");
        $scope.$apply();
    }
});
```

The equivalent function in SanteDB's API:

```javascript
try {
    $scope.alert = await SanteDB.resources.mail.getAsync($stateParams.alertId);
    $scope.alert.body = $scope.alert.body.replace("\n", "<br/>");
    $scope.$apply();
}
catch(e) {
    console.error(e);
    $rootScope.errorHandler(e);
}
```

This means all code on your user interface must be upgraded to use the new APIs.

#### New AngularJS Controls

The new AngularJS controls are also updated from the original OpenIZ controls. Whereas OpenIZ required the user to manually implement things like name editing, address editing, etc. SanteDB now allows for simple entry:

```markup
<edit-name name="patient.name" no-add="true" />
```

