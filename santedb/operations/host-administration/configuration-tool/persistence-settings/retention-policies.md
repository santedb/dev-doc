# Retention Policies

Administrators can specify optional retention policies which use the ADO.NET Data Archiving and Shipping service in order to purge/obsolete data which is no longer clinically relevant. 

When enabled, the retention policy feature will create a JOB on system startup which will ensure that data is retained according to the administrator configured policies.

![](<../../../../../.gitbook/assets/image (435).png>)

| Option             | Description                                                                                                                                          | Example                           |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------- |
| Policy Variables   | Allows the specification of variables (like cutoff dates, environment variables, etc.) which can be used in the retention policy definitions.        | Collection if .NET C# Expressions |
| Policy Definitions | The specification of one or more data retention policies which the policy retention service will apply.                                              | See Below                         |
| Job Status         | When ENABLED the retention policy will be enabled on system startup.                                                                                 | ENABLED \| DISABLED               |
| Repeat             | The days of the week when the scheduled job of retention should be applied.                                                                          | Day of Week                       |
| Start On           | The date/time when the job should be started (time indicates the time the job will start)                                                            | DateTime                          |
| Stop On            | The date/time when the job should no longer be triggered                                                                                             | DateTime                          |
| Stop This Event    | When true, the Stop On property is enforced, when false the job will run on the schedule indefinitely.                                               | Boolean                           |
| Interval           | If you want to run the retention job on an interval rather than on a particular kickoff time each day of the week, use the interval here in seconds. | Number                            |
| Use Interval       | When TRUE the interval value is used and the job is triggered on a regular timer. When FALSE the job is scheduled to execute on the Start On time.   | Boolean                           |

