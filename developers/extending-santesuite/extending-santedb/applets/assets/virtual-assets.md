# Virtual Assets

An applet's manifest can declare virtual assets which are exposed via a known URL but actually combine a series of other assets into a single file. This is useful if you want to break up large JavaScript files but expose them as one file.

To define a virtual asset, use the following registration for the asset in the manifest.xml file:

```markup
<asset name="js/controllers.js" mimeType="text/javascript">
    <virtual>
      <include>js/controllers/.*\.js</include>
    </virtual>
  </asset>
```

In this example, when the browser requests http://\<host>/\<applet-id>/js/controllers.js the contents of the applet in js/controllers/\*.js will be rendered out as a single JavaScript file.
