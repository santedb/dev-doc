# Reports Centre

{% hint style="info" %}
This feature is only available on SanteDB Version 3.0
{% endhint %}

The SanteDB [Business Intelligence Services](../../../developers/extending-santesuite/extending-santedb/applets/business-intelligence-bi-assets/), provide developers with a method of expressing queries which can aggregate, pivot and otherwise generate informative reports for users. These reports vary depending on the configuration of SanteDB, however they are all available through the report centre on the SanteDB administrative panel menu.

## Report Centre

The report centre home screen provides a list of all developed public reports that have been installed on the SanteDB server.

<figure><img src="../../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

You may launch a report with the **View** option.

## Viewing Report

When clicking the View button the report launcher will be opened. Depending on whether the report accepts parameters or not, you will be presented with either the report rendering or a parameter input screen as shown below:

<figure><img src="../../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

The types of parameters will depend on the report, the general types of report parameters are:

* **Dates**: Represented as a date/calendar input. These allow the user to select a date and typically ignore time portions of the parameter.
* **Date/Time:** Represented as a combination of a date, and a timestamp. These allow the user to select an exact moment in time.
* **Coded:** Represented as a drop down list, allowing users to select an input from a predetermined list. The drop-down list is limited to 200 options.
* **Numeric:** Represented as a number spinner. These allow users to select a number within a particular range.
* **Text:** Represented as a simple text input allowing for any freetext parameter to be supplied.

After selecting the parameters, the report output can be previewed by pressing **Apply**.

<figure><img src="../../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Only the first 1,000 results are rendered in the preview. The search bar in the tabular preview will only filter on the first 1,000 results.
{% endhint %}

### Downloading Data

The entirety of the dataset can be downloaded by selecting the **Download** option and selecting the desired output format.

<figure><img src="../../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Large datasets (>10,000 results) on output formats such as XLSX may consume large amounts of memory.
{% endhint %}

