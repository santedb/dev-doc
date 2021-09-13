# Customization & Branding

Many of the core SanteMPI applets allow for easy customization of their default look and feel, routes, etc. This customization is done by giving your assets a higher priority than the built in assets in SanteMPI.

#### Overriding Default UI Text

You can override any textual elements in SanteDB by setting the priority on the string you'd like to override. For example, if you'd like to change the title of the default landing page you can use:

```text
<strings lang="en">
    <string key="ui.title" priority="1">My Custom SanteMPI App</string>
```

#### Overriding UI Elements

You can override certain portions of the default user interface by setting a priority on your state with the same route name. For example, if you want to provide a custom login screen you merely need to override the login route

```text
<div xmlns="http://www.w3.org/1999/xhtml" xmlns:sdb="http://santedb.org/applet" 
     ng-controller="LoginController"
     ng-init="login = { grant_type: 'password', forbidPin: true, welcomeMessage: undefined, noSession: false }">
    <sdb:style static="false">/org.santedb.admin/css/admin.css</sdb:style>
    <sdb:style static="false">/org.santedb.admin/css/sb-admin.css</sdb:style>
    <sdb:state name="login" priority="1">
        <sdb:url>/login?returnState</sdb:url>
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

Now, whenever an asset wishes to prompt the user to login, your custom login page will be displayed in place of the original.

