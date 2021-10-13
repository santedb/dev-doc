# Health Data Services Interface

The Health Data Services Interface configuration panel allows administrators to configure the behaviors and allowed resources on the HDSI. 

![](<../../../../../.gitbook/assets/image (434) (1).png>)

When **Allowed Resources** are not configured, the HDSI allows all resources to be accessed on the HDSI (it exposes the resources on the HDSI). When an **Allowed Resources** value is configured, only those resources listed in the collection are exposed on the interface. 

{% hint style="info" %}
The **Allowed Resources** setting enables system administrators to reduce the attack surface area of their CDR by selectively disabling CDR data which can be exposed on the server.
{% endhint %}
