# Pub/Sub Manager

The Pub/Sub manager allows administrators to control the [publish-subscribe-architecture.md](../../../../santedb/software-architecture/publish-subscribe-architecture.md "mention")subscriptions registered in the iCDR instance.&#x20;

## Subscription List

The publish/subscribe manager shows a list of all registered subscriptions. This view allows administrators to quickly enable or disable outbound subscriptions from the iCDR or dCDR instance.

![](<../../../../.gitbook/assets/image (434) (1) (1) (1) (1).png>)

The commands on this screen:

* Create - Allows administrators to create new subscription definitions with the related endpoint information.
* Edit - Change the settings of an already registered subscription definition.
* Enable / Disable - When a subscription is active, it is sending data out to the configured endpoints, when the subscription is inactive the subscription is registered, but will not send notifications. The enable/disable button permits the administrator to change this setting.
* Delete / Un-Delete - Allows an administrator to remove a subscription, and to restore it.

## Creating/Editing a Subscription

When creating a subscription the administrator will be prompted to enter settings related to the subscription which is being created.

### Subscription Metadata

Subscription metadata is used to describe the subscription to other administrators using the iCDR solution.

![](<../../../../.gitbook/assets/image (448) (1) (1) (1) (1) (1).png>)

* Name - A unique named identifier for the subscription which appear in logs
* Description - A short description of the subscription, its purpose, why it exists.
* Support Contact - The person who should be contact when/if the subscription fails.

### Subscription Filter

Next, administrators should specify the criteria under which the notification is triggered.&#x20;

![](<../../../../.gitbook/assets/image (435) (1) (1) (1) (1) (1) (1) (1).png>)

* Applies To - The resource which this subscription applies to
* Event(s) - The persistence events when the recipient should be notified
* When Criteria - The filters for new events which should be applied when new data is received. These dictate when the recipient will be notified.

#### Preventing Bouncing

Sometimes when a SanteDB product notifies an external party of a registration of an event, the notified party will respond back with updates it would like to perform. In this scenario, we do not want the SanteDB server to re-send the object back to the system which made the change.&#x20;

To prevent this behavior, filter the subscription based on the principal/application that last created the version of the object. For example, if the API key of the object which is the target of the notification is `APP_THAT_SENDS_STUFF`we can instruct the pub/sub layer to prevent sending any updates received by `APP_THAT_SENDS_STUFF`to the application:

<figure><img src="../../../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

### Endpoint Settings

The endpoint settings are used to control how and when the messages are sent to the remote endpoint.&#x20;

![](<../../../../.gitbook/assets/image (447) (1) (1) (1) (1).png>)

* Not Before - The date/time when the endpoint should start receiving messages from the iCDR
* Not After - The date/time when the endpoint should stop receiving messages from the iCDR
* Endpoint - The remote endpoint (url) where the notification dispatches should be sent
* Dispatcher - The dispatching class to be used for formatting messages and authentication with the remote endpoint.
* Custom Settings - Key/value pairs which are passed to the dispatcher to control settings related to authentication, message formatting, etc.

#### Dispatchers

| fhir-message                    | Send messages using FHIR messaging (a message bundle with content)                                     | <ul><li>Content-Type - Controls the format with <code>application/fhir+xml</code> sending XML format messages and <code>application/fhir+json</code> sending JSON</li><li>MessageId - Controls the message identifier sent in the FHIR message</li></ul>                                                                                                             |
| ------------------------------- | ------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| fhir-rest-hook                  | Send messages using FHIR REST operations such as POST, PUT, DELETE.                                    | <ul><li>Content-Type - Controls the format with <code>application/fhir+xml</code> sending XML format messages and <code>application/fhir+json</code> sending JSON</li></ul>                                                                                                                                                                                          |
| hl7-pat-id-source (SanteDB 3.x) | Sends LLP messages to a remote HL7v2 receiver using ADT^A01 , ADT^A08 and ADT^A40 (optionally ADT^A38) | <ul><li>MSH8 - The MSH8 security setting to be used</li><li>Transport - <code>sllp</code> to use secure LLP and <code>llp</code> to use unsecure llp</li><li>MSH34 - The MSH3 | MSH4 to send (default is the SanteDB server's)</li><li>SendAs - <code>Client</code> if sending ADT^A01, ADT^A08, ADT^A40 messages, or <code>Server</code> if using ADT^A38</li></ul> |

## Related Topics

{% content-ref url="../../../../developers/santedb-software-publishers/publish-subscribe.md" %}
[publish-subscribe.md](../../../../developers/santedb-software-publishers/publish-subscribe.md)
{% endcontent-ref %}

{% content-ref url="dispatcher-queue.md" %}
[dispatcher-queue.md](dispatcher-queue.md)
{% endcontent-ref %}

