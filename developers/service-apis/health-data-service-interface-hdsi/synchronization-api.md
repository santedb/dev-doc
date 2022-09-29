# Synchronization API

{% hint style="danger" %}
This page is part of a proposed enhancement to SanteDB's APIs. It may not be present in the current version of SanteDB
{% endhint %}

## Synchronization API

OpenIZ and SanteDB's iCDR and dCDR subscription model was classically based on the [hdsi-query-syntax](hdsi-query-syntax/ "mention") using the ?\_subscription parameter which allows clients to control the type of data that they wished to receive.&#x20;

This API was useful as it allowed the server to define subscriptions with custom, optimized SQL, however it was sub-optimal in that several requests would need to be made to each resource which the dCDR would want to download.&#x20;

The new API proposes a solution whereby a client's onboarding process creates a registration of selected subscriptions which the client is creating. The server may then decide the best order of loading, and can use the UNION functionality and stored queries to obtain the list of data which needs to be subscribed to.&#x20;

It also allows the server to "prepare" a subscription batch&#x20;
