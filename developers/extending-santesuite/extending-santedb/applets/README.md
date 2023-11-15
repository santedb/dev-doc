---
description: >-
  In SanteDB, an applet represents a collection of HTML5, JavaScript, and XML
  files which are used to solve a particular problem.
---

# Applets

Applets are the foundation of extending SanteDB. An applet can contain:

* Custom user interface components (using CSS, JavaScript, AngularJS, and HTML5)
* Custom Business Rules written using the SanteDB Business Rules engine
* Custom Reports written using the embedded reporting engine (those which operate in all SanteDB environments)
* Clinical Decision Support Rules (CDSS) written using XML formatted when/then commands
* Custom View-Model files which instruct SanteDB how to render JSON to consumer applications
* Translations and localization settings for a particular locale
* Custom matching configurations used for the SanteDB Matching Algorithms
* Clinical Template Definitions which contain the validation rules, entry and render forms, and structure of clinical data

### Recommended Tooling

In order to develop SanteDB applets, you'll need a few tools:

* **The SanteDB Software Development Kit** - Contains the necessary tools to debug and package your applet.
* **An HTML5 + JavaScript Editor -** We recommend [Visual Studio Code](https://code.visualstudio.com/), but any editor will do the trick
* **(Optional) An XML Editor -** An XML editor is highly recommended, especially if you're going to be doing heavy editing of SanteDB's CDSS, BI, DataSet, ViewModel or Subscription services.

### Getting Started

Getting started with SanteDB applet authoring is easy

1. Download and install the latest SanteDB SDK: [https://github.com/santedb/santedb-sdk/releases](https://github.com/santedb/santedb-sdk/releases)
2. Clone the starter applet source code: [https://github.com/santedb/applet-starter](https://github.com/santedb/applet-starter)
3. Start your favorite code editor!

To test your applet, you can run the Applet Debugging Environment (ADE)&#x20;

```
sdb-ade --applet=path_to_source_code --ref=org.santedb.core --ref=org.santedb.uicore ...
```

## Topics

{% content-ref url="applet-use-and-lifecycle.md" %}
[applet-use-and-lifecycle.md](applet-use-and-lifecycle.md)
{% endcontent-ref %}

{% content-ref url="applet-sdk/" %}
[applet-sdk](applet-sdk/)
{% endcontent-ref %}

{% content-ref url="applet-structure.md" %}
[applet-structure.md](applet-structure.md)
{% endcontent-ref %}

{% content-ref url="javascript-api.md" %}
[javascript-api.md](javascript-api.md)
{% endcontent-ref %}

{% content-ref url="business-intelligence-bi-assets/" %}
[business-intelligence-bi-assets](business-intelligence-bi-assets/)
{% endcontent-ref %}

{% content-ref url="localization.md" %}
[localization.md](localization.md)
{% endcontent-ref %}

{% content-ref url="customization-and-branding.md" %}
[customization-and-branding.md](customization-and-branding.md)
{% endcontent-ref %}

{% content-ref url="assets/" %}
[assets](assets/)
{% endcontent-ref %}

{% content-ref url="angularjs.md" %}
[angularjs.md](angularjs.md)
{% endcontent-ref %}

{% content-ref url="cdss-protocols.md" %}
[cdss-protocols.md](cdss-protocols.md)
{% endcontent-ref %}

{% content-ref url="business-rules.md" %}
[business-rules.md](business-rules.md)
{% endcontent-ref %}

{% content-ref url="distributing-data.md" %}
[distributing-data.md](distributing-data.md)
{% endcontent-ref %}

{% content-ref url="applet-solution-packages.md" %}
[applet-solution-packages.md](applet-solution-packages.md)
{% endcontent-ref %}

{% content-ref url="../../../../santempi/recipes/" %}
[recipes](../../../../santempi/recipes/)
{% endcontent-ref %}
