# Security Policy Management

As mentioned in the SanteDB architecture, SanteDB provides a robust policy infrastructure. This policy infrastructure can describe policies which a user account must be granted in order to execute an action (permission policies) or to access a particular piece of data within the database structure. The administrative portal provides several key functions related to the administration of policies. To see the counterpart to these functions from the perspective of the [SanteDB iCDR Admin Console](../../../operations/server-administration/santedb-icdr-admin-console/), see the [Policy Administration](../../../operations/server-administration/santedb-icdr-admin-console/policy-administration.md) page.

## Reviewing Policies

SanteDB comes pre-installed with all the permission policies it requires to operate appropriately, and also with a few data policies ("Restricted Data" is one). Most of these policies are demanded by SanteDB system components, and therefore cannot be deleted by the system administrator, and thus are marked as "Readonly".

![](<../../../.gitbook/assets/image (61).png>)

You can also see the policy hierarchy using the policy's OID. The way that this works, is quite simple, if a component or piece of data DEMANDS a policy at a lower level in the OID,  and the user is granted a higher level, the decision is inherited.&#x20;

| IANA PEN    | Mohawk | Research | Health | SanteDB | Policies | MDM | Write |
| ----------- | ------ | -------- | ------ | ------- | -------- | --- | ----- |
| 1.3.6.1.4.1 | 33349  | 3        | 1      | 5       | 9        | 6   |       |
| 1.3.6.1.4.1 | 33349  | 3        | 1      | 5       | 9        | 6   | 1     |

Here, if the user is granted all MDM : 1.3.6.1.4.1.33349.3.1.5.9.2.6 , and a function demands WRITE MDM 1.3.6.1.4.1.33349.3.1.5.9.2.6.1, the decision is GRANT.

## Creating A New Policy

If you wanted to create a new policy, for example, to control access to HIV records, you could select the **Create** button.&#x20;

![](<../../../.gitbook/assets/1 (2).jpg>)

You'll then be presented with the new policy ID screen. Fill out the fields appropriately and click the **Save** button.(The OID and Name fields are required and must be filled out)

{% hint style="info" %}
Carefully plan out our policy OIDs, it is important to keep in mind the hierarchy of the policy enforcement system in SanteDB so you don't accidentally allow a particular group access to a confidential record.
{% endhint %}

{% hint style="info" %}
You can make a policy overridable by checking the override option while creating the policy. Keep in mind that once saved , your policy cannot be edited. This is to ensure the consistency of audits.
{% endhint %}

{% hint style="info" %}
Override Option

when an app/device/user has the ELEVATE grant on a policy for example "Access HIV ART Number" , the system will by default throw an error and deny access. If the user is assigned GRANT on the " Override" policy and the policy itself has "Override" , then then the user/app may prompt the user for a purpose of use , their username and password and then they can re-authenticate themselves requesting permission to that policy.
{% endhint %}



![](<../../../.gitbook/assets/CreatePolicyForm (2).png>)

Once created, your policy can be assigned to any device, group, or application. For example, if you wanted to DENY access to HIV records you would do so in the UI. Any records tagged with this policy would be disclosed, masked, or not disclosed based on the policy permission you've set.

![](<../../../.gitbook/assets/image (63).png>)

##

