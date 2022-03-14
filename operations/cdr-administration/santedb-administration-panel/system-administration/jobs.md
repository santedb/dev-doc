# Jobs

The jobs panel shows the available system jobs within the SanteDB server. System jobs are implementations of the `IJob` interface and may be run on a schedule (such as cleaning or maintenance jobs) or might be one off jobs. Jobs are shown with their last execution time and current status.

{% hint style="info" %}
Jobs are run in the background and can execute without blocking other processes. The Jobs panel can be used to see the last time a job was run, its outcome and to manually kickstart the job.
{% endhint %}

The jobs panel summary shows the list of jobs registered on the dCDR or iCDR.

![](<../../../../.gitbook/assets/image (437) (1) (1) (1) (1).png>)

The columns for the job indicate:

* Name - The name and description of the job which is represented.
* Schedule / Repeat - Indicates the configured schedule for the job.
* Current State - Shows the current status of the job.
  * Running - The job is currently executing in the background
  * Aborted - The job started, however due to an error it had to stop
  * Not Yet Run - The job has never been run
  * Complete - The job has completed successfully
  * Cancelled - The job was cancelled before it could be completed
* Actions - Allows the administrator to control the job:
  * Run - Run the job immediately
  * Cancel - (if supported) Send a cancellation request to the job
  * Schedule - Modify or set the job's schedule

## Running a Job

When you run a system job you will be prompted to provide any job parameters (if any) which will control the execution of the task.

![](<../../../../.gitbook/assets/image (432) (1) (1) (1) (1) (1) (1) (1).png>)

After setting parameters and pressing `Ok` administrators will be asked to confirm the execution of the job.

## Scheduling Jobs

{% hint style="info" %}
This feature is only available in administrative portals > version 2.1.165
{% endhint %}

SanteDB jobs can be run on a schedule. The schedule for jobs are persisted (by default) in the `xcron.xml` file in the installation directory (this can be changed by registering or implementing `IJobScheduleManager`).

Scheduling a job is performed by clicking on the `Schedule` button on the job summary page.

![](<../../../../.gitbook/assets/image (441) (1) (1) (1).png>)

Upon opening the job schedule, a window will appear allowing the user to configure a job schedule. There are two methods for setting a job schedule:

### Interval Schedule

An interval schedule is used when the job should be run on a regular timed interval. This timer is started when the SanteDB host process is started and repeats at the specified timing.

![](<../../../../.gitbook/assets/image (433) (1) (1).png>)

### Calendar Schedule

A calendar schedule should be used whenever the job needs to be executed on a repeated calendar day. For example, to refresh the materialized views at 11 PM every day starting January 26, 2022.

![](<../../../../.gitbook/assets/image (435) (1) (1) (1) (1) (1).png>)

If a future date or time is specified, then the job will only run&#x20;
