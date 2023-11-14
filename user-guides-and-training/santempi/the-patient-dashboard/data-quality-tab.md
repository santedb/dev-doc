# Data Quality Tab

Whenever a patient has been sent to the SanteMPI system (or edited in the user interface), the the data quality plugin will perform validation according to rules configured on the SanteDB server.&#x20;

When data quality rules are detected as violated, the issue is flagged in a data quality extension (see: [data-quality-services.md](../../../operations/server-administration/host-configuration-file/data-quality-services.md "mention")), and the user interface will reflect these rules.

![](<../../../.gitbook/assets/image (421).png>)

The data quality rule will have:

* Level - Indicates the severity of the data quality violation
* Classification - Indicates the system class of the violation
* ID - Indicates the unique identifier of the rule (configured by the implementation) which triggered the rule violation
* Information - Human readable information about the violation.

## Severity

The severity column will indicate the impact that the data quality violation has:

| Level       | Description                                                                                                                                                                             |
| ----------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Error       | These types of data quality rules don't usually appear in the data quality tab since a violation with level of `Error` causes the inbound message to be rejected by the SanteDB server. |
| Warning     | Indicates that the data quality issue needs to be investigated (may represent an issue with data collection) however it does not prevent the information from being stored.             |
| Information | Indicates the data quality issue is for information purposes only - there is no action required.                                                                                        |

## Classification

The classification indicates the class of detected issue (such as privacy, security, etc.)

| Classification           | Description                                                                                    | Examples                                                                                                                                                                  |
| ------------------------ | ---------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Security                 | The issue was raised due to a security constraint on the object.                               | <ul><li>A field was edited/provided which the sender does not have permission to set.</li></ul>                                                                           |
| Formal Constraint        | The issue was raised due to a formal constraint violation.                                     | <ul><li>Birthdates in the future</li><li>Demographic data does not meet minimum data set.</li><li>Missing or invalid data detected (checksums, patterns, etc.).</li></ul> |
| Improper Code            | The issue was raised because an improper / invalid code was used.                              | <ul><li>Use of a Gender code in Marital Status Field</li></ul>                                                                                                            |
| Other / Unclassified     | Other or unclassified reason for the issue being raised.                                       |                                                                                                                                                                           |
| Already Done             | The issue is being raised because an action was already performed.                             | <ul><li>Attempt was made to re-apply an action to the record.</li></ul>                                                                                                   |
| Improper Data/Validation | The issue is raised because the supplied data is improper for the context in which it is used. | <ul><li>Last menstrual period observation on a male patient</li><li>Weight observation on a fetus.</li></ul>                                                              |
| Business Rule            | The issue is raised due to a custom business rule failing validation.                          | <ul><li>Any custom business rule provided by the implementation was violated.</li></ul>                                                                                   |
| Patient Safety           | The issue is raised because the data represents a patient safety concern.                      | <ul><li>Attempting to administer a substance to a patient where an AEFI was previously recorded.</li></ul>                                                                |
| Patient Privacy          | The issue is raised because the data or action represents a patient privacy concern.           | <ul><li>Attempting to change a protected field.</li><li>Attempting to break the glass without appropriate permission.</li></ul>                                           |

