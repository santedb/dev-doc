# HTML Widgets

The default SanteDB user interfaces (for SanteEMR, SanteGuard, SanteMPI, etc.) all provide UI extension points through widgets. A widget is a custom portlet which is rendered inside of another context.&#x20;

For example, if you wanted to collect setup information related to your particular SanteDB based project on the initial configuration of the SanteDB software, you could create a widget to extend the configuration system rather than re-writing or forking the entire configuration system.

In order to configure a widget the following things must be present:

1. The root element must be a \<div> in the **http://www.w3.org/1999/xhtml** namespace
2. The file must be XHTML (well formed XML)
3. The namespace **http://santedb.org/applet**_ _must be declared
4. If the widget requires a custom controller, the controller must be loaded using oc-lazy-load attribute on the root element.
5. The widget must be declared with the widget element (see below for an example).

```markup
<div xmlns="http://www.w3.org/1999/xhtml" 
  xmlns:sdb="http://santedb.org/applet"
>
  <sdb:widget name="org.example.widget" type="Tab" order="10" context="org.santedb.configuration">
    <sdb:demand>1.3.6.1</sdb:demand>
    <sdb:icon>fas fa-cog</sdb:icon>
    <sdb:guard>!scopedObject.tag</sdb:guard>
    <sdb:description lang="en">Example Widget</sdb:description>
  </sdb:widget>
  <div>
    Hello {{ scopedObject.name.Legal | name }}
  </div>
</div>
```

### Widget Configuration

The contents of the `<sdb:widget/>` element control the widget's rendering and visibility.&#x20;

| Property  | Description                                                                                                                                                    | Example                                                                                                     |
| --------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------- |
| @name     | The name of the widget                                                                                                                                         | org.widgets.mywidget                                                                                        |
| @type     | The type of widget (tab or panel)                                                                                                                              | Tab \| Panel                                                                                                |
| @order    | The preferred / default order of the widget                                                                                                                    | 10                                                                                                          |
| @context  | The widget context (where the widget is rendered)                                                                                                              | org.santedb.configuration                                                                                   |
| @altViews | <p>Alternate views the widget supports. These are exposed </p><p>to the widget in <code>{{panel.view}}</code></p>                                              | <p>None - No Alternate Views</p><p>Edit - Shows a pencil in widget</p><p>Settings - Shows cog in widget</p> |
| @priority | <p>Used to override the default implementations of core</p><p>widgets. The widget identifier with the highest priority</p><p>is the one that is displayed.</p> | `priority="100"`                                                                                            |
| icon      | The icon for the widget                                                                                                                                        | fas fa-cog                                                                                                  |
| demand    | The permission(s) needed to enable/view the widget.                                                                                                            |                                                                                                             |
| guard     | A guard condition when the widget should appear                                                                                                                |                                                                                                             |

### Widget Contexts

There are several contexts in which widgets appear.

| Context                          | Type  | Description                                                                   |
| -------------------------------- | ----- | ----------------------------------------------------------------------------- |
| org.santedb.config.init          | Tab   | Allows addition of configuration panels on initial configuration screen.      |
| org.santedb.config               | Tab   | Allows addition of configuration panels to the configuration screen.          |
| org.santedb.patient              | Tab   | Allows addition of a tab on the patient profile screen.                       |
| org.santedb.place                | Tab   | Allows addition of tabs on the place profile screen                           |
| org.santedb.user                 | Tab   | Allows addition of tabs on the user profile screen                            |
| org.santedb.patient.demographics | Panel | One or more panels to appear in the "demographics" tab of the patient screen. |
| org.santedb.mdm                  | Panel | One or more panels to appear in the Master Data Management tab                |

### Scoped Object

All widgets are passed a `scopedObject` reference in JavaScript which can be used to access the primary focal object of the context where the widget appears. For example, if your widget context is `org.santedb.patient`, then the `scopedObject` would be the patient which is currently being viewed.

### Widget Controllers

Due to the manner in which widgets are loaded (at render time), the use of `<sdb:script>` does not work. It is therefore required to use the `oc-lazy-load` AngularJS component to load the controllers you require. For example, to add a custom controller:

```markup
<div xmlns="http://www.w3.org/1999/xhtml" 
  xmlns:sdb="http://santedb.org/applet"
  oc-lazy-load="{ name: 'ExampleWidgetController', files: ['/org.example/controllers/widget.js'] }"
>
  <sdb:widget name="org.example.widget" type="Tab" order="10" context="org.santedb.configuration">
    <!-- Truncated for space -->
  </sdb:widget>
  <div ng-controller="ExampleWidgetController">
  </div>
</div>
```

## Hosting Widgets

You can add your own widget extension points by adding one of the two widget hosting panels to your user interface. The two controls are widget-panels and widget-tabs which will render panels or tabs depending on your context.

```markup
<widget-panels context-name="'my.sample.panels'" scoped-object="currentPatient"/>
<widget-tabs context-name="'my.sample.tabs'" scoped-object="currentPatient"/>
```
