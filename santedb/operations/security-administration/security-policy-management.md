# Security Policy Management

As mentioned in the SanteDB architecture, SanteDB provides a robust policy infrastructure. This policy infrastructure can describe policies which a user account must be granted in order to execute an action \(permission policies\) or to access a particular piece of data within the database structure. 

## Reviewing Policies

SanteDB comes pre-installed with all the permission policies it requires to operate appropriately, and also with a few data policies \("Restricted Data" is one\). Most of these policies are demanded by SanteDB system components, and therefore cannot be deleted by the system administrator, and thus are marked as "Readonly".

![](../../../.gitbook/assets/image%20%2865%29.png)

You can also see the policy hierarchy using the policy's OID. The way that this works, is quite simple, if a component or piece of data DEMANDS a policy at a lower level in the OID,  and the user is granted a higher level, the decision is inherited. 

| IANA PEN | Mohawk | Research | Health | SanteDB | Policies | MDM | Write |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1.3.6.1.4.1 | 33349 | 3 | 1 | 5 | 9 | 6 |  |
| 1.3.6.1.4.1 | 33349 | 3 | 1 | 5 | 9 | 6 | 1 |

Here, if the user is granted all MDM : 1.3.6.1.4.1.33349.3.1.5.9.2.6 , and a function demands WRITE MDM 1.3.6.1.4.1.33349.3.1.5.9.2.6.1, the decision is GRANT.

## Creating A New Policy

If you wanted to create a new policy, for example, to control access to HIV records. You could select the **Create Policy** button. You'll then be presented with the new policy ID screen:

![](../../../.gitbook/assets/image%20%2895%29.png)

{% hint style="info" %}
Carefully plan out our policy OIDs, it is important to keep in mind the hierarchy of the policy enforcement system in SanteDB so you don't accidentally allow a particular group access to a confidential record.
{% endhint %}

Once created, your policy can be assigned to any device, group, or application. For example, if you wanted to DENY access to HIV records you would do so in the UI. Any records tagged with this policy would be disclosed, masked, or not disclosed based on the policy permission you've set.

![](../../../.gitbook/assets/image%20%2815%29.png)

