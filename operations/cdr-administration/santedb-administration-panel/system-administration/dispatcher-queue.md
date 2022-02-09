# Dispatcher Queue

Whenever SanteDB needs to send data using a standards based interfaces to systems that aren't the current instance of the iCDR or the dCDR the messages will be placed into a dispatcher queue.&#x20;

{% hint style="info" %}
Dispatcher queues differ from synchronization queues used on the dCDR in that they do not support reconciliation of conflicts or subscription management. Dispatcher queuest are intended from remote targets that aren't SanteDB such as FHIR endpoints, HL7v2 endpoints or GS1 endpoints.
{% endhint %}

![](<../../../../.gitbook/assets/image (430) (1) (1) (1) (1) (1).png>)

Users can opt to `Resubmit` a queue, which instructs the dCDR or iCDR to take all messages from a dead letter queue and place them back into the primary queue for re-submission. Additionally administrators may `Purge` a queue, which instructs the dCDR or iCDR to purge all data in the waiting dispatch list.

SanteDB may be used with a queueing technology like MSMQ or a simple queue like the default file based queue. Common queues used in the SanteDB server are:

* `sys.pubsub` - Used for all outbound dispatches to standards based pub-sub broker requests. These are things like patient registrations, notifications of data changing, etc.
* `sys.audit` - Used for dispatching audits to remote systems.
* `sys.ami` - Used by direct connect dCDR instances to queue administrative command messages to the central iCDR.
