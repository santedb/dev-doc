# Edit CDSS Library

{% hint style="info" %}
This page documents a user interface which is used for the entry of CDSS Definitions. It does not cover the complex topic of defining or writing CDSS rules and logic. Readers should familiarize themselves with the [CDSS Definitions](../../../../developers/applets/cdss-protocols/cdss-definitions.md) wiki topic prior to continuing this page.
{% endhint %}

SanteEMR's administration portal allows administrators to edit CDSS definition rules directly in the administrative panel. This can be accessed via the CDSS library index, or by clicking the **Edit** option while viewing a CDSS library.&#x20;

<figure><img src="../../../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

## Editing CDSS Rules

CDSS rules can be directly edited in the **Source** tab. This tab provides a rudimentary code editor with syntax highlighting and interactive validation of the CDSS source code.&#x20;

Errors validation issues with the CDSS rules are provided in the **Errors/Issues** panel. They are indicated both in the editor in the gutter area (beside the line number) and as a list of all issues. CDSS authors can directly access offending line numbers by clicking on the error.

<figure><img src="../../../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

The editor supports several shortcuts which are provided below:

* `CTRL+F` - Find text - Search for text in the code editor
* `CTRL+H` - Replace Text - Search for text in the code editor and replace it with new text
* `CTRL+S` - Publish/Save CDSS - Send a copy of the CDSS library to the iCDR server and save it
* `F9` - Test - Test the CDSS library

## Testing CDSS Rules

CDSS rules can be tested by clicking on the **Test Rules** tab or pressing **F9**.&#x20;

{% hint style="info" %}
You can test CDSS rules without saving or publishing them to the iCDR server. This is useful for debugging and diagnosing CDSS logic prior to committing the logic.
{% endhint %}

The test screen provides base inputs for the testing session as shown below.

<figure><img src="../../../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

The process for testing is as follows:

1. Select an object type (usually Patient) which will serve as the input to the CDSS library.
2. Select whether an existing record from the SanteDB CDR database should be used, or whether a new object is to be used.
3. Specify any additionally parameters by entering the parameter name and value, then pressing the ADD button.
4. Press the **Run** button

After the rule has been executed the output of the rule will be shown as illustrated below.

<figure><img src="../../../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

### Output Target

The output target tab is used to show the resulting input object after the CDSS library rules have been executed. If your logic contains any unbound **assign** statements (for example: setting interpretation codes) they will be reflected in the object produced here.

<figure><img src="../../../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

### Proposals

The proposals tab is used to show the `Act` instances which were proposed. These acts will appear in the patient encounter (if the encounter is occurring between `startTime` and `stopTime` of the act). This should be used to diagnose your `propose` statements in your decision logic.

<figure><img src="../../../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

### Raised Issues

The raised issues tab is used to show the output of any `raise` statements in the CDSS library. These issues will appear as alerts on the patient encounter screen. Any alerts which are flagged as `danger` or `error` must be manually cleared (or signed off) by the discharging physician.

<figure><img src="../../../../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

### Debug Trace

The debug trace is used for advanced diagnostics of **how** the CDSS library came to propose the acts and raise the issues it has. It allows users to delve into the call process and to tune their CDSS library based on the inputs provided. The debug trace provides similar functionality to an `EXPLAIN` command in SQL provides.

<figure><img src="../../../../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>
