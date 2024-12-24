# Clinical Templates

{% hint style="info" %}
This page documents a feature in SanteDB 3.0 with SanteEMR 3.0 plugins enabled and activated on the administrative panel.
{% endhint %}

SanteEMR clinical data templates exist as a method of further specializing acts (observations, procedures, substance administrations) into a specific templated model and a series of views which allow for the editing, and viewing of those types of acts. Templates combine:

* A model template which:
  * Defines the default and fixed values for entry of data
  * The information or components within the act which is to be populated
* Views which define:
  * Data entry formlets used for data capture of information in the template
  * Views which are used for displaying the information in a clinical summary or in a detail view

Examples of a clinical template may be:

* A standardized input for childhood milestone development (`CodedObservations`)
* A pain scale input&#x20;

## Template Summary

The templates which are installed on the system are located in the **SanteEMR > Templates** area of the administrative panel.&#x20;

<figure><img src="../../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

The template library allows an administrator to:

* Create a **New** clinical data template and model from scratch
* **Upload** a clinical data template that was prepared by another developer or downloaded from another instance of SanteEMR
* Search for clinical data templates which are installed on the SanteEMR instance
* **View** and **Edit** existing clinical data templates
* **Remove** a clinical data template
* **Enable** or **Disable** a clinical template

{% hint style="warning" %}
Clinical templates which are marked as **Read-only** are typically built-in or system templates. Removing these templates may result in them being re-installed when an applet is upgraded
{% endhint %}

### Uploading a Template

To upload an existing template into the SanteEMR instance, use the **Upload** option. Select the downloaded template definition file and press upload.

<figure><img src="../../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

{% hint style="warning" %}
Uploading a template which has the same identifier as a system or readonly template will result in an error. To upload an override of a built-in template, remove the readonly template and then upload the replacement ensuring that the `version` is a higher number than `2`(which is used by the default readonly template installers.
{% endhint %}

### Creating a Template

To create a template, press the **New** button on the summary screen. Enter the required information and press **Save**

<figure><img src="../../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

<table><thead><tr><th>Field</th><th width="332">Description</th><th>Example</th></tr></thead><tbody><tr><td>mnemonic</td><td>A unique name which is used by developers to identify the template in program code.</td><td><code>org.example.pain</code></td></tr><tr><td>Universal ID</td><td>An OID which is used when acts created using this template are disclosed over a standardized API  (FHIR, HL7, etc.)</td><td><code>1.3.xxxxxx</code>(PEN)<br><code>2.25.xxxxxx</code>(UUID)</td></tr><tr><td>Name</td><td>A short human readable name which is used in drop-downs in the EMR interface when adding new acts to an encounter.</td><td><code>Pain Scale</code></td></tr><tr><td>Applies To</td><td>One or more encounter types (see: <a data-mention href="visit-types-and-flows.md">visit-types-and-flows.md</a>) where this template can be added to.</td><td></td></tr></tbody></table>

## Clinical Template Details

The template details page is used to edit and/or modify existing template definitions in the SanteEMR instance.

<figure><img src="../../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

The details page has three tabs in a default installation of the SanteEMR:

* **Properties:** Used to edit the core properties (from the create template modal)
* **Model / Template:** Used to define the RIM model which is used to create new instances
* **Views / Forms:** Used to define the view, edit forms of the template in the SanteEMR clinic user interface.

### Model / Template

The model/template tab in view mode will show the current definition as described in the template definition. The view shows an object explorer of the defined object which allows an administrator to expand and view the interpreted RIM model as the CDR will construct new data.

<figure><img src="../../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

#### Editing the Model / Template

{% hint style="info" %}
Read-only or system templates will provide an option to edit the model or template.
{% endhint %}

Clicking on the pencil icon will activate the editor for the RIM template, which is expressed in JSON view model (see: [conceptual-data-model](../../../santedb/data-and-information-architecture/conceptual-data-model/ "mention")).&#x20;

<figure><img src="../../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

The editor supports the **CTRL+S** keyboard shortcut for saving the current contents of the editor model.&#x20;

* Hovering over a UUID will load the definition of the UUID and display it for the developer ![](<../../../.gitbook/assets/image (12).png>)
* The RIM model is automatically loaded along with the documentation for each of the properties \
  ![](<../../../.gitbook/assets/image (13).png>)
* Errors with the model are indicated with an error marker at the location where the error occurred ![](<../../../.gitbook/assets/image (14).png>)

{% hint style="info" %}
Only valid models (with no issue markers) can be saved using **CTRL+S** or the **Submit** option
{% endhint %}

### Views / Forms

#### Adding a New View / Form

When the views and forms panel is in edit mode, new views can be created, this is done by clicking on the drop down and indicating the type of view that is being created, and pressing **Add.**

<figure><img src="../../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

The view types are:

* **Entry:** Used when a single data element is being captured today
* **Back Entry:** Used for multiple data elements being back-entered
* **Detail View:** The view as it appears in the encounter detail view
* **Summary View:** The view as it appears in the encounter summary

When a new view or form is added, the default format is a **Simplified** form creation language. The editor allows developers to switch to HTML which provides more features, however does require more work and knowledge of HTML and the CDR.

<figure><img src="../../../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

Like the RIM editor, the **CTRL+S** key will save the current view. The live preview of the form as it would appear in the EMR user interface is rendered on the right-hand side of the screen.

#### Editing in HTML

Developers can also switch their views to HTML, this allows complete control over the behavior and rendering of the input form. Editing in HTML uses the same controls as described in the [angularjs.md](../../../developers/extending-santesuite/extending-santedb/applets/angularjs.md "mention") section.&#x20;

{% hint style="info" %}
You can start your form in the simplified view to get a general layout of the input format and then convert the layout to HTML automatically to do fine tuning.
{% endhint %}

The simplified view to render a simple input would be expressed as:

```xml
<SimplifiedViewDefinition xmlns="http://santedb.org/model/template/view">
    <grid>
        <row>
            <label size="md" color="primary">Respiration Rate</label>
            <flex>
                <input size="md" type="number" min="1" binding="value" cdss="true" name="observedValue"></input>
                <span>Per Minute</span>
            </flex>
        </row>
        <row>
            <info type="info">
                <title>Tips for Measuring Respiration Rate</title>
                <list>
                    <item>Ensure that the patient is in a sitting position and is resting comfortably</item>
                    <item>Use a stopwatch and a stethoscope to count the respiration rate</item>
                </list>
            </info>
        </row>
    </grid>
</SimplifiedViewDefinition>
```

In HTML this same view is expressed as:

```html
<?xml version="1.0" encoding="utf-8"?>
<div xmlns="http://www.w3.org/1999/xhtml">
  <div class="container-fluid">
    <div class="form-group row">
      <label class="control-label col-xs-12 col-lg-6 col-xl-3 text-primary">Respiration Rate</label>
      <div class="d-flex flex-row justify-content-start">
        <div class="flex-grow-1">
          <input type="number" min="1" cdss-interactive="act" ng-model="act.value" name="observedValue" class="form-control" />
          <div class="text-danger" ng-if="(ownerForm || $parent.ownerForm || $parent.$parent.ownerForm).observedValue.$error.min">
            <i class="fas fa-fw fa-exclamation-triangle"> </i>{{ 'ui.error.min' | i18n }}</div>
        </div>
        <span class="flex-grow-1">Per Minute</span>
      </div>
    </div>
    <div class="form-group row">
      <div class="d-flex justify-content-left alert alert-info">
        <h5 class="m-0 p-2">
          <i class="fas fa-fw fa-info-circle m-auto d-block" />
        </h5>
        <div class="d-flex flex-column mx-1">
          <h5 class="mb-1 m-0 p-0">Tips for Measuring Respiration Rate</h5>
          <ul class="">
            <li>Ensure that the patient is in a sitting position and is resting comfortably</li>
            <li>Use a stopwatch and a stethoscope to count the respiration rate</li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</div>
```

