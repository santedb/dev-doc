# HTML Widgets

The default SanteDB user interfaces \(for SanteEMR, SanteGuard, SanteMPI, etc.\) all provide UI extension points through widgets. A widget is a custom portlet which is rendered inside of another context. 

For example, if you wanted to collect setup information related to your particular SanteDB based project on the initial configuration of the SanteDB software, you could create a widget to extend the configuration system rather than re-writing or forking the entire configuration system.

In order to configure a widget the following things must be present:

1. The root element must be a &lt;div&gt; in the **http://www.w3.org/1999/xhtml** namespace
2. The file must be XHTML \(well formed XML\)
3. The namespace **http://santedb.org/applet** __must be declared
4. If the widget requires a custom controller, the controller must be loaded using oc-lazy-load attribute on the root element.
5. The widget must be declared with the widget element \(see below for an example\).

```markup
<div xmlns="http://www.w3.org/1999/xhtml" 
  xmlns:sdb="http://santedb.org/applet"
  oc-lazy-load="{ name: 'ExampleWidgetController', files: ['/org.example/controllers/widget.js'] }"
>
  <sdb:widget name="org.example.widget" type="Tab" context="Configuration">
    <sdb:icon>fas fa-cog</sdb:icon>
    <sdb:description lang="en">Example Widget</sdb:description>
  </sdb:widget>
  <div ng-controller="ExampleWidgetController">
  </div>
</div>
```



