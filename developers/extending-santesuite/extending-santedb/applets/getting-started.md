# Getting Started

This article will illustrate the use of the SanteDB dCDR SDK to write a portable SanteDB dCDR applet.&#x20;

You should follow the [installing-the-dcdr-sdk.md](../../../../installation/installation-1/deployment/software-deployment/disconnected-gateway/installing-the-dcdr-sdk.md "mention") before completing this exercise.

## Obtain the Starter Code

Next, you'll need to clone or create an applet. You can clone the starter applet from [https://github.com/santedb/applet-starter](https://github.com/santedb/applet-starter) in any directory of your choice.

![](<../../../../.gitbook/assets/image (193).png>)

## Hello World!

If you re-run the command `sdb-ade --ref=santedb.admin.sln.pak --applet=path-to-applet-starter` you'll notice that upon login you see the administrative panel. This is because the --ref= is instructing the SDK that your module is extending the admin panel.

To debug just the applet-starter applet you can instead reference just the core plugins:

```
sdb-ade --ref=santedb.core.sln.pak --applet=path-to-applet-starter
```

The browser will launch with the basic login.html contents, which you can login with demoadmin/@Elbonia123.

{% hint style="info" %}
The login screen is shown because the index.html view demands login permission to be rendered. By default the dCDR interface will display the default AngularJS route of /
{% endhint %}

After logging in, you should see the welcome message:

![](<../../../../.gitbook/assets/image (192).png>)

### Code Editing

You can now edit the files in your favorite HTML/JavaScript editor. After editing a file you simply need to press the refresh button on the browser window. We can also update the code to query some patients from the database, if we modify the contents of index.html:

```markup
<div>
    <form name="searchForm" ng-submit="doSearch(searchForm)" method="dialog">
        Search For: <input 
            required="required" minlength="3" maxlength="30" 
            type="text" ng-model="searchTerm" />
        <button type="submit">{{ 'ui.action.search' | i18n }}</button>
    </form>
    <table border="1">
        <tr ng-repeat="result in results.resource">
            <td>{{ result.name | name }}</td>
        </tr>
    </table>
</div>
```

This code:

* Creates a new form which calls the doSearch function in the controller
* Allows the user to enter a text search term
* Renders the results in the bundle

{% hint style="info" %}
All HTML in SanteDB must be well-formed XHTML placed in the [http://www.w3.org/1999/xhtml](http://www.w3.org/1999/xhtml) namespace.
{% endhint %}

We can then edit the index.js controller file to actually perform our search:

```javascript
$scope.doSearch = doSearch;

// Perform a search 
async function doSearch(searchForm) {
    if(searchForm.$invalid) {
        alert("Invalid Input!");
        return;
    }

    try {
        $scope.results = await SanteDB.resources.patient.findAsync({ "name.component.value" : `~${$scope.searchTerm}` });
    } catch (e) {
        $rootScope.errorHandler(e);
    }
}
```

This code:

* Validates that the form has no issues
* Calls the SanteDB API to find all patients (SanteDB.resources.patient.findAsync) who has any name (name.component.value) is approximately the output (the \~ indicator)
* Assigns the results of the call to the scoped results variable

![](<../../../../.gitbook/assets/image (191).png>)

### Next Steps

For an example of a more complex applet which extends the underlying administrative panel, you can clone the elb-mpi project and launch the debugger with that codebase:

```javascript
sdb-ade --ref=santedb.admin.sln.pak --applet=path-to-elb-mpi
```

When launching this you should be presented with the Elbonia customizations of the MPI administrative panel.

![](<../../../../.gitbook/assets/image (195).png>)

### Useful Hints

* You can reset your debugging environment with the `sdb-ade --reset` option
* You can setup different servers/environments by adding the --name= option, for example, you can setup a PROD and STAGE debugging environment by using `sdb-ade --ref=XXX --name=PROD` and `sdb-ade --ref=YYY --name=STAGE`
* You can change the configuration of your debugging environment and/or see offline files in the following directory:
  * %localappdata%\log => Logs from the debugging environment
  * %localappdata%\SDBADE => Data files (databases, preferences, etc.)
  * %appdata%\SDBADE => Configuration files

## Related Topics

{% content-ref url="./" %}
[.](./)
{% endcontent-ref %}

