# System Administration

The SanteDB system administration area of the SanteDB administration panel allows administrators to determine overall system health of the iCDR (Realm Service) or the local dCDR instance running (Local Service).

## Probes

The probes screen shows a summary of all installed `IDiagnosticsProbe` implementations on the dCDR or iCDR to which the administration panel is connected. These probes provide a real-time reading of available operating system and internal system data.

![](<../../../.gitbook/assets/image (422) (1).png>)

Probes are used to diagnose the overall health and status of the server. Any plugin can implement an `IDiagnosticsProbe` for any reading it wishes to emit to administrators.&#x20;

By default the probes on SanteDB are:

| Probe       | Description                                                                                                                                                                                                                                                              | Components                                                                                                                                                                                                                                                               |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Thread Pool | SanteDB iCDR and dCDR use their own ThreadPool for asynchronous operations. This implementation allows cross-platform use of a consistent thread pool without consuming the underlying .NET thread pool.                                                                 | <p>Pool Size: The maximum number of concurrent actions allowed in the thread pool</p><p>Pool Use: The number of worker threads which are currently busy servicing requests</p><p>Queue Depth: The number of waiting tasks which are waiting for an available worker.</p> |
| Machine     | The machine probe shows underlying use statistics from the host environment on which the iCDR or dCDR is running. Currently these probes values are only available on Windows Operating Systems.                                                                         | <p>CPU Use: The % use of all CPUs on the iCDR or dCDR machine</p><p>Memory Use: The % use of system memory on the iCDR or dCDR machine</p><p>Disk Use: The % busy time of the disk infrastructure on the iCDR or dCDR machine</p><p></p>                                 |
| REST Pool   | The REST server pool probe is used for diagnosing issues on the REST based API. In SanteDB the REST APIs use their own thread pool (separate from the system thread pool), this thread pool use statistic shows the occupation of HTTP requests waiting to be processed. |                                                                                                                                                                                                                                                                          |

## Jobs

The jobs panel shows the available system jobs within the SanteDB server. System jobs are implementations of the `IJob` interface and may be run on a schedule (such as cleaning or maintenance jobs) or might be one off jobs. Jobs are shown with their last execution time and current status.

{% hint style="info" %}
Jobs are run in the background and can execute without blocking other processes. The Jobs panel can be used to see the last time a job was run, its outcome and to manually kickstart the job.
{% endhint %}

&#x20;

![](<../../../.gitbook/assets/image (440).png>)

### Running a Job

When you run a system job you will be prompted to provide any job parameters (if any) which will control the execution of the task.

![](<../../../.gitbook/assets/image (432) (1).png>)

After setting parameters and pressing `Ok` administrators will be asked to confirm the execution of the job.

## Logs

SanteDB server logs can be accessed using the Logs menu in the System panel. Logs allow system administrators to access either dCDR or iCDR log files from the web user interface directly.

![](<../../../.gitbook/assets/image (424) (1).png>)

When an administrator opens a log, a quick preview of the log contents are shown, and an option to download the entirety of the system log is provided.

![](<../../../.gitbook/assets/image (425) (1) (1).png>)

## Server Status

The Server Status page allows system administrators to quickly gather server information for the execution environment. Server status will show:

* The current versions of the SanteDB software running on the server
* The installed plugins and applets installed on the SanteDB dCDR and iCDR
* The applets which have been enabled in the SanteDB server
* The installed services and their current state.

![](<../../../.gitbook/assets/image (427) (1).png>)

{% hint style="info" %}
Administrators can enable or disable services on the local dCDR instance. This is not recommended on a Windows or Docker instance of SanteDB and is intended primarily for the Disconnected Gateway and Android applications. The setting of these enable/disable flags requires a restart of the host environment to take full effect.
{% endhint %}

## Dispatcher Queues

Whenever SanteDB needs to send data using a standards based interfaces to systems that aren't the current instance of the iCDR or the dCDR the messages will be placed into a dispatcher queue.&#x20;

{% hint style="info" %}
Dispatcher queues differ from synchronization queues used on the dCDR in that they do not support reconciliation of conflicts or subscription management. Dispatcher queuest are intended from remote targets that aren't SanteDB such as FHIR endpoints, HL7v2 endpoints or GS1 endpoints.
{% endhint %}

![](<../../../.gitbook/assets/image (430) (1) (1).png>)

Users can opt to `Resubmit` a queue, which instructs the dCDR or iCDR to take all messages from a dead letter queue and place them back into the primary queue for re-submission. Additionally administrators may `Purge` a queue, which instructs the dCDR or iCDR to purge all data in the waiting dispatch list.

SanteDB may be used with a queueing technology like MSMQ or a simple queue like the default file based queue. Common queues used in the SanteDB server are:

* `sys.pubsub` - Used for all outbound dispatches to standards based pub-sub broker requests. These are things like patient registrations, notifications of data changing, etc.
* `sys.audit` - Used for dispatching audits to remote systems.
* `sys.ami` - Used by direct connect dCDR instances to queue administrative command messages to the central iCDR.



