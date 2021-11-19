# Publish/Subscribe

SanteDB supports subscribing to resource events via the creation of `Subscription` resource instances.&#x20;

{% hint style="info" %}
Currently the SanteDB iCDR PubSub layer does not use persistence queues for retry/resubmit. This feature is currently under construction, as of version 2.1.x PubSub requests are realtime push notifications and the use of an external reliable delivery method is recommended.
{% endhint %}

## Creating Subscriptions

The underlying implementation of the FHIR Subscription mechanism is the SanteDB PubSub broker, when a `Subscription` resource is created the SanteDB iCDR service interacts with the PubSub broker to:

* Create a new channel definition with the appropriate endpoint and authentication information,&#x20;
* Creates a new subscription definition with the appropriate filter criteria,
* Activates the subscription if `active` is set to true.

For example, consider this subscription request

```javascript
{
  "resourceType": "Subscription",
  "id": "my_subscription",
  "status": "active",
  "contact": [
    {
      "system": "phone",
      "value": "180086626362"
    }
  ],
  "end": "2025-01-01T00:00:00Z",
  "reason": "Monitor Creation of Female Patients",
  "criteria": "Patient?gender=female",
  "channel": {
    "type": "rest-hook",
    "endpoint": "http://localhost:8989/fhir/Patient",
    "payload": "application/fhir+json",
    "header": [
      "Authorization: Bearer secret-token-abc-123"
    ]
  }
}
```

This subscription definition would:

* Create a new channel definition pointing at http://localhost:8989&#x20;
  * Content/Type would be added (`application/fhir+json`) to the channel definition
  * Authorization header (`bearer secret-token-abc-123`) added to the channel definition
  * The channel dispatcher would be mapped from `rest-hook` to the `FhirRestHookDispatcher`
* Create a new subscription definition :
  * FHIR resource type `Patient` would be mapped to target `SanteDB.Core.Model.Roles.Patient`
  * Filter criteria `gender=female` would be mapped to HDSI filter `genderConcept.referenceTerm.mnemonic=female`
  * Subscription would be activated
  * Subscription would have a `notAfter` time set of `2025-01-01`

### Supported Dispatchers

The SanteDB iCDR supports the following dispatchers on the channel:

| Type           | Channel Scheme    | Dispatcher                              |
| -------------- | ----------------- | --------------------------------------- |
| rest-hook      | fhir-rest-http:// | `FhirPubSubRestHookDispatcher`          |
| message        | fhir-msg-http://  | `FhirPubSubMessageDispatcher`           |
| sms            | sms://            | Default handler for SMS messages        |
| email          | mailto://         | Default handler for e-mail messages     |
| llp (extended) | llp://            | Notify using HL7v2 LL (extended option) |
