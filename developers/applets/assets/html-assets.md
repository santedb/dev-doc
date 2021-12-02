# HTML Assets

In a SanteDB applet, a page, partial or piece of HTML is designed around strict XHTML and must be annotated so the proper routing is setup on the AngularJS stack.

Rules for HTML assets in an applet are:

1. Must be well-formed XML
2. Root element must be in **http://www.w3.org/1999/xhtml** namespace
3. Root element must be a \<div>, \<table>, \<span>, or \<p> tag.

## Empty HTML Asset Template

At a bare minimum, an empty HTML asset should appear with the following structure:

```markup
<div xmlns="http://www.w3.org/1999/xhtml">
    ...
</div>
```

From here the asset can be loaded by the applet collection manager.

## Extended Asset Tags

You can also decorate your HTML asset with a series of tags in the `http://santedb.org/applet` namespace in order to add functionality. Before decorating your asset, be sure to declare the namespace:

```markup
<div xmlns="http://www.w3.org/1999/xhtml" 
    xmlns:sdb="http://santedb.org/applet">
    ...
</div>
```

### Including Scripts

One of the extended tags allows you to either inject a JavaScript include into the header of the already rendered page (a static reference) or to load the reference on demand when the asset it requested. This is done using the script tag.&#x20;

The following example includes a controller JS file, dynamically loaded:

```markup
<div xmlns="http://www.w3.org/1999/xhtml" 
    xmlns:sdb="http://santedb.org/applet">
    ...
    <sdb:script static="false">~/controllers/index.js</sdb:script>
    ...
</div>
```

### Including CSS

You can also use the style tag to inject a CSS reference into the already rendered HTML page (this is useful if you are creating a custom theme or using a third party library).

```markup
<div xmlns="http://www.w3.org/1999/xhtml" 
    xmlns:sdb="http://santedb.org/applet">
    ...
    <sdb:style>~/css/theme.css</sdb:style>
    ...
</div>
```

### Angular Routes / States

One of the more powerful features of the SanteDB user interface, is that it uses an AngularJS SPA architecture. SanteDB's rendering engine will automatically generate a routes.js file based on the applets which are loaded into the execution context.&#x20;

In order to register your page and a route, you need to create an AngularJS state, this is done by decorating your asset with an asset tag:

```markup
<div xmlns="http://www.w3.org/1999/xhtml" 
    xmlns:sdb="http://santedb.org/applet">
    ...
    <sdb:state name="example" priority="0">
        <sdb:title lang="en">Example</sdb:title>
        <sdb:url>/example</sdb:url>
        ...
    </sdb:state>
</div>
```

This registers a new state with name "example" at the URL /example into the ng-route context. This page can now be referenced by using:

```markup
<a ui-sref="example">Go to Example</a>
```

The sdb:title element is used by the breadcrumb plugin to render the path to the specified page, as well as to change the title of the browser window (if applicable).

{% hint style="info" %}
HTML asset states which need to be abstract can be created by adding the **abstract** attribute to the **sdb:state** element.
{% endhint %}

Furthermore, we can demand a specific permission be present for the current user in order to allow navigation:

```markup
<div xmlns="http://www.w3.org/1999/xhtml" 
    xmlns:sdb="http://santedb.org/applet">
    ...
    <sdb:state name="example">
        <sdb:url>/example</sdb:url>
        <sdb:demand>1.3.6.1.4.1.33349.3.1.5.9.2.1</sdb:demand>
        ...
    </sdb:state>
</div>
```

This has the following behavior:

* If there is no session, then the policy evaluation equates to ELEVATE and a 401 is returned (where SanteDB will by default, navigate to state 'login')
* If there is a session, and the user has the policy, the evaluation is GRANT and a HTTP 200 is returned and the asset HTML is provided to the client
* If there is a session, and the user has the specified policy but on when elevated, then the ELEVATE decision (401) is returned with a re-authentication request.
* If there is a session and the user does not have access then DENY is evaluated and an HTTP 403 is returned.

Finally, if your route requires a controller, you can have this dynamically executed / requested by using the sdb:view element:

```markup
<div xmlns="http://www.w3.org/1999/xhtml" 
    xmlns:sdb="http://santedb.org/applet">
    ...
    <sdb:state name="example">
        <sdb:url>/example</sdb:url>
        <sdb:demand>1.3.6.1.4.1.33349.3.1.5.9.2.1</sdb:demand>
        <sdb:view>
            <sdb:controller>ExampleController</sdb:controller>
        </sdb:view>
    </sdb:state>
</div>
```

A completed example page may be:

```markup
<div xmlns="http://www.w3.org/1999/xhtml" 
    xmlns:sdb="http://santedb.org/applet">
    <sdb:script static="false">~/controllers/index.js</sdb:script>
    <sdb:style>~/css/theme.css</sdb:style>
    <sdb:state name="example">
        <sdb:title lang="en">Example Page</sdb:title>
        <sdb:url>/example</sdb:url>
        <sdb:demand>1.3.6.1.4.1.33349.3.1.5.9.2.1</sdb:demand>
        <sdb:view>
            <sdb:controller>ExampleController</sdb:controller>
        </sdb:view>
    </sdb:state>
    {{ helloMessage }}
</div>
```

#### Overriding Routes

There may arise a need to override a page/view that is already registered in an underlying component. This is done with the `priority` attribute. For example, to override the default login page:

```markup
<div xmlns="http://www.w3.org/1999/xhtml" xmlns:sdb="http://santedb.org/applet" 
     ng-controller="LoginController"
     ng-init="login = { grant_type: 'password', forbidPin: true, welcomeMessage: undefined, noSession: false }">
    <sdb:style static="false">/org.santedb.admin/css/admin.css</sdb:style>
    <sdb:style static="false">/org.santedb.admin/css/sb-admin.css</sdb:style>
    <sdb:state name="login" priority="1">
        <sdb:url>/login</sdb:url>
        <sdb:view>
        </sdb:view>
    </sdb:state>
    Quick and Dirty Login Screen:
    
    <form class="form" ng-submit="doLogin(loginForm)" name="loginForm">
          <!-- #include virtual="/org.santedb.uicore/partials/security/login.html" -->
          <br/>
          <button type="submit" id="loginButton" class="btn btn-lg btn-primary">
                 <i class="fa fa-check"></i> {{ 'ui.action.login' | i18n }}
         </button>
    </form>
</div>
```

{% hint style="info" %}
You should **never fork** the core SanteDB applets to override user interface elements. This can cause compatibility and management headaches in operations. It is recommended you use the priority mechanism described here.
{% endhint %}

### Angular Controller

If using the default user interface framework, you must attach the AngularJS controller to the **santedb** module.

```javascript
angular.module('santedb').controller('ExampleController', ["$scope", function($scope) {
    $scope.helloMessage = 'Hello World!';
}]);
```

## Content Security Policy

SanteDB applets must adhere to CSP rules, failure to adhere to these rules in your applets not working properly in deployment.&#x20;

### Script References

Any scripts that you want to load should be loaded with the syntax:

```markup
<sdb:script static="false|true">path_to_script</sdb:script>
```

The SanteDB system will place a unique NONCE on this element rendered into HTML and will append the corresponding NONCE to the JS file as it is served out.

### Inline Scripts

Inline scripts like the one illustrated below are strictly prohibited, and will throw an error in the browser. It is recommended you use the guidance here [https://csp.withgoogle.com/docs/adopting-csp.html](https://csp.withgoogle.com/docs/adopting-csp.html) , to overcome this.

```markup
<button onclick="foo()">Foo!</button>
```

### Browser APIs

SanteDB's disconnected client software blocks access to the browser APIs for camera, geolocation, accelerometer, payment, and autoplay. SanteDB provides its own APIs for calling these services.

This allows SanteDB to restrict access to these services on a per-user basis in scenarios where devices are shared between users. SanteDB also audits access to these sensitive services in its audit repository.

