# Jobs

The jobs panel shows the available system jobs within the SanteDB server. System jobs are implementations of the `IJob` interface and may be run on a schedule (such as cleaning or maintenance jobs) or might be one off jobs. Jobs are shown with their last execution time and current status.

{% hint style="info" %}
Jobs are run in the background and can execute without blocking other processes. The Jobs panel can be used to see the last time a job was run, its outcome and to manually kickstart the job.
{% endhint %}

&#x20;

![](<../../../../.gitbook/assets/image (440) (1) (1) (1).png>)

## Running a Job

When you run a system job you will be prompted to provide any job parameters (if any) which will control the execution of the task.

![](<../../../../.gitbook/assets/image (432) (1) (1).png>)

After setting parameters and pressing `Ok` administrators will be asked to confirm the execution of the job.
