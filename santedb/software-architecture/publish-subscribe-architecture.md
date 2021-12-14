# Publish / Subscribe Architecture

SanteDB iCDR and dCDR supports basic subscription management. This facility allows external parties to subscribe (via a subscription) to data persistence events, at which they they will receive a notification (via a channel) using one of the available dispatch formats.

![](<../../.gitbook/assets/image (439).png>)

The components of the publish and subscribe architecture are:

| Repository Service     | The primary persistence repositories. These are responsible for the persisting and loading of data to/from the primary data persistence layer.                                                                                                                             |                                                                                                                  |
| ---------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| Record Merging Service | The service which is responsible for merging and unmerging records, detecting duplicates, etc.                                                                                                                                                                             | <p>MDM Record Merging <br>SIM Record Merging</p>                                                                 |
| PubSub Broker          | The publish/subscribe broker is responsible for brokering the publish and subscribe events to/from the manager service. The broker subscribes to events from the repository and merging service, ad then queues these messages on the configured `IDispatcherQueueService` |                                                                                                                  |
| Dispatcher Queue       | The dispatcher queue service is responsible for interacting with a persistent queue technology and enqueueing and dequeuing those messages.                                                                                                                                | <p>MSMQ Dispatcher Queue<br>File Dispatcher Queue</p>                                                            |
| PubSub Manager         | The pub/sub manager service is responsible for maintaining the registration of subscriptions and the related channel configuration.                                                                                                                                        | Ado PubSubManager                                                                                                |
| Dispatcher Factory     | The dispatcher factory is responsible for constructing dispatcher instances based on a particular outbound message format.                                                                                                                                                 | <p>FHIR Message Dispatcher Factory<br>FHIR Rest Hook Dispatcher Factory<br>(coming) HL7v2 Dispatcher Factory</p> |
| Dispatcher             | The dispatcher is the class which is responsible for converting the RIM based internal formatted notification to an appropriate notification in the format specified for the receiver.                                                                                     | <p>FHIR Message Dispatcher<br>FHIR RestHook Dispatcher</p>                                                       |

## Publish/Subscribe Manager Schema

The PubSubManager stores data for subscriptions and channels in a concise schema.&#x20;

![](<../../.gitbook/assets/image (427) (1).png>)

### Subscriptions

Subscriptions are defined with a target resource (such as Patient, Act, Entity, Person, Place, etc.). The subscription defines one or more events and a series of filters which will trigger the issuance of a notification to the receiver.

The following notification events can be subscribed.

| Create   | Triggered when a subscribed resource's `Inserted` event is fired.                    |
| -------- | ------------------------------------------------------------------------------------ |
| Update   | Triggered when the subscribed resource's `Updated` event is fired.                   |
| Delete   | Triggered when the subscribed resource's `Obsoleted` event is fired.                 |
| Merge    | Triggered when the subscribed resource's merging service fires the `Merged` event.   |
| UnMerged | Triggered when the subscribed resource's merging service fires the `UnMerged` event. |

{% hint style="info" %}
The notifications for each event are triggered by any internal update/change to data in the iCDR. This means that updates, merges, etc. received via FHIR, HL7v2, or even the user interfaces will trigger notifications.
{% endhint %}

### Channels

A channel defines the mechanism to notify the receiver of the publish notification. The channel specifies the endpoint URL (mailto:, sms:, http:, llp:, etc.) the dispatcher to be used, and any settings. Settings are stored as key/value pairs which, depending on the dispatcher will be used to determine the channel format, authorization, etc.
