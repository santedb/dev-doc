# Applet Configuration

The AppletConfigurationSection is responsible for configuring the applet loading and validation process. The configuration is illustrated below.

```markup
  <section xsi:type="AppletConfigurationSection" 
    appletDirectory=".\applets" 
    allowUnsignedApplets="true">
    <trustedPublishers>
      <add>82C63E1E9B87578D0727E871D7613F2F0FAF683B</add>
      <add>4326A4421216AC254DA93DC61B93160B08925BB1</add>
    </trustedPublishers>    
  </section>
```

With options:

| Option | Use |
| :--- | :--- |
| @appletDirectory | Allows your deployment to use a different location for storing/loading applets. This is useful in a web-farm environment where multiple iCDR instances must access the same applets. |
| @allowUnsignedApplets | When true, allows for debugging applets and/or untrusted applets which have not been signed to be loaded and execute code. |
| &lt;trustedPublishers&gt; | Lists of one or more X509 code signing certificate thumbprints to trust when loading/validating applets. |

{% hint style="info" %}
Be cautious about enabling unsigned applets and/or adding trusted publishers. Applet files are permitted to operate/execute JavaScript code on the server on any data event \(business rule trigger\). Only install applets from sources you trust.
{% endhint %}

