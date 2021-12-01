# Retention Policies

Administrators can specify optional retention policies which use the ADO.NET Data Archiving and Shipping service in order to purge/obsolete data which is no longer clinically relevant.&#x20;

When enabled, the retention policy feature will create a JOB on system startup which will ensure that data is retained according to the administrator configured policies.

![](<../../../../.gitbook/assets/image (436) (1) (1).png>)

| Option             | Description                                                                                                                                          | Example                                                             |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------- |
| Policy Variables   | Allows the specification of variables (like cutoff dates, environment variables, etc.) which can be used in the retention policy definitions.        | Collection if .NET C# Expressions                                   |
| Policy Definitions | The specification of one or more data retention policies which the policy retention service will apply.                                              | See: [Retention Policy Definition](retention-policies.md#undefined) |
| Job Status         | When ENABLED the retention policy will be enabled on system startup.                                                                                 | ENABLED \| DISABLED                                                 |
| Repeat             | The days of the week when the scheduled job of retention should be applied.                                                                          | Day of Week                                                         |
| Start On           | The date/time when the job should be started (time indicates the time the job will start)                                                            | DateTime                                                            |
| Stop On            | The date/time when the job should no longer be triggered                                                                                             | DateTime                                                            |
| Stop This Event    | When true, the Stop On property is enforced, when false the job will run on the schedule indefinitely.                                               | Boolean                                                             |
| Interval           | If you want to run the retention job on an interval rather than on a particular kickoff time each day of the week, use the interval here in seconds. | Number                                                              |
| Use Interval       | When TRUE the interval value is used and the job is triggered on a regular timer. When FALSE the job is scheduled to execute on the Start On time.   | Boolean                                                             |

## Retention Policy Definition

The retention service requires the definition of retention policies which need to be applied.&#x20;

![](<../../../../.gitbook/assets/image (429) (1).png>)

| Option           | Description                                                                                                                                                                                                             | Example                                                                                     |
| ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| Applies To       | <p>The resource type that the policy applies to. </p><p>Note: SanteDB Resources use inheritance so a binding to <strong>Person</strong> applies to <strong>Patient, Person,</strong> and <strong>Provider</strong> </p> | `Patient`                                                                                   |
| Exclude Filter   | The HDSI query filters of objects which DO NOT APPLY to this retention policy.                                                                                                                                          | See: [HDSI Query Syntax](../../../../developers/service-apis/hl7-fhir/hdsi-query-syntax.md) |
| Include Filter   | The HDSI query filters for objects which DO APPLY to this retention policy.                                                                                                                                             | See: [HDSI Query Syntax](../../../../developers/service-apis/hl7-fhir/hdsi-query-syntax.md) |
| Name             | An informative name to show in logs and notifications.                                                                                                                                                                  | `Males > 10 yo`                                                                             |
| Retention Policy | The actual policy which should be applied to the retention of data.                                                                                                                                                     | See: [Retention Policies](retention-policies.md#undefined)                                  |

### Retention Policies

The retention policy on a policy definition indicates the action that the service should take on data which matches **Include Filter** but is not in **Exclude Filter**.

| Policy   | Description                                                                                                                                                                      | Example Action                       |
| -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------ |
| Purge    | Purges (permanently erases) data from the primary database. The data is no longer stored. For versioned resources, a resource pointer is maintained with a status key of PURGED. | Purge all Obsolete Patients          |
| Obsolete | Obsoletes (logically erases) data from the primary database. The data continues to exist in the primary database however it does not appear in user interfaces.                  | Obsolete all Patients > 10 years old |
| Archive  | Copies the data from the primary database (in the ADO.NET Data Persistence Service configuration) to the archive database (in the ADO.NET Archiving and Shipping configuration)  |                                      |
