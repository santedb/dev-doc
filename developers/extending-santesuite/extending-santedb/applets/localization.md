# Localization

The core SanteDB applets are designed to easily be localized and branded to suit your particular deployment of SanteDB.&#x20;

## Localizing Your Applets

When writing your applets, there are a variety of ways to make localization and branding of your applet easier. First, in all HTML assets you can use the i18n service in Angular to localize your asset.&#x20;

```markup
<strong>{{ 'my.ui.local.string' | i18n}}</strong>
```

{% hint style="warning" %}
It is recommended you use the manifest file and i18n service as SanteDB will pre-translate the file before sending it to the browser and will cache the result. This reduces the amount of processing power required for repeat viewing of the page.
{% endhint %}

You should then register **my.ui.local.string** in the applet's manifest file.

```markup
<strings lang="en">
    <string key="my.ui.local.string">My Local String</string>
```

If you want to fetch a string from JavaScript in the current locale, you can use the localization service

```javascript
if(!valid) {
    alert(SanteDB.locale.getString("my.ui.local.error"));
    
```

## Switch Locales

By default, SanteDB will switch the current locale of the user interface to that preferred by the user when they authenticate. You can also manually set the locale by calling

```javascript
SanteDB.locale.setLocale('en');
```

When you call this, a cookie is set in the browser which controls the rendering on the server side. However, this is the lowest order of preference for the server. In short, the server will render assets using the following preference:

1. The user's preference (stored at : `UserEntity.languageCommunication`) is used, if the user has no preference then,
2. The `lang` cookie provided by the browser, if there is no setting then
3. The value of `Accept-Language` HTTP header sent by the browser, if not sent then
4. The configured server preference (set in the SanteDB.config.xml file)

## Registering New Locales

Locales are registered using the applet `manifest.xml`, within the manifest, you can specify one or more assets (css, javascript, etc.) to be loaded for the particular locale. For example, to define a localization for Esperanto:

```markup
<AppletManifest xmlns="http://santedb.org/applet">
    <info id="org.santedb.sample">
        ...
    </info>
    
    ...
    
  <locales>
    <locale code="eo">
      <asset>/org.santedb.sample/i18n/angular-locale_eo.js</asset>
      <asset>/org.santedb.sample/i18n/santedb-eo.js</asset>
    </locale>
  </locales>
```

This instructs the SanteDB application framework to register a new locale "EO" and load the two supplied assets whenever the user interface is switched to locale eo.&#x20;

{% hint style="info" %}
The locale JavaScript files can be your own settings for SanteDB specific objects or they can be included libraries from common javascript plugins.&#x20;
{% endhint %}

## Overriding Default Translations

The core SanteDB applets provide default translations for all core SanteDB concepts. Sometimes, depending on the context, these need to be changed. This is supported in the `manifest.xml` file using the `priority` attribute on your translation, for example, to override the default title of the Administrative Panel you could use:

```markup
<strings lang="en">
    <string key="ui.title" priority="100">My Custom Title</string>
```

{% hint style="info" %}
It is recommended you **never fork** the core applets to change translations, this is very difficult to maintain and we cannot guarantee compatibility.
{% endhint %}

## Mozilla Pontoon

You may also collect your strings in an Android style `strings.xml` format, this allows common tools like [Mozilla Pontoon](https://pontoon.santesuite.net) to edit your strings. In order to use this method, you should have an applet structure collecting strings under locale directories such as `locales/en/strings.xml` and `locales/fr/strings.xml` , or you may use `i18n/en/strings.xml` and `i18n/en/strings.xml`.

Once complete, you can reference your strings files in the manifest (as shown in the example below):

{% tabs %}
{% tab title="manifest.xml" %}
```markup
<strings lang="eo" extern="i18n/eo/strings.xml" />
```
{% endtab %}

{% tab title="strings.xml" %}
```markup
<resources>
    <string name="my.ui.local.string">My Local String</string>
</resources>
```
{% endtab %}
{% endtabs %}

Finally, you should create a file called `i18n.toml` in your applet to allow Mozilla Pontoon to import your strings.

```
basepath = "."
locales = [ "en", "fr", "es", "sw", "it", "my" ] 
[[paths]]
    refernece = "i18n/en/strings.xml"
    l10n = "i18n/{locale}/strings.xml"
```

Once completed, you can setup a project in your Pontoon server which points to your github repository (see: [Localizing your projects](https://mozilla-pontoon.readthedocs.io/en/latest/user/localizing-your-projects.html)) and use the sync feature. The strings located in your `strings.xml` file should be reflected in the Mozilla Pontoon user interface where **Context** indicates the name of your resource string:

![](<../../../../.gitbook/assets/image (402).png>)

{% hint style="info" %}
When you use a `strings.xml` file for your translations, you cannot override the default translations with `priority=` mechanism supported by the `manifest.xml`
{% endhint %}

### Community Translations

SanteDB community translations are collected via the SanteDB Pontoon service. The following process is used:

1. As the SanteDB community implements new features they add them to the appropriate `strings.xml` file with an English translation.
2. Prior to a new minor release the SanteDB team merges the new terms from `develop` branch into the `i18n` branch - and the new strings become available in SanteDB.
3. The community can contribute translations of the new strings into the `i18n` branch
4. Prior to a major release the `i18n` branch is merged into `develop`(all community translations are present)
5. The build is validated and the `develop` branch is merged into `master` where a new release is packaged.
