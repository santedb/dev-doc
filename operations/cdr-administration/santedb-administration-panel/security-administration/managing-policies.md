# Managing Policies

SanteDB uses a policy based access control scheme (see: [#policy-access-control-architecture](../../../../santedb/security-architecture.md#policy-access-control-architecture "mention")), each SanteDB policy is used to either:

1. Restrict a user's ability to perform an action (an action policy), or
2. Restrict a user's ability to see data (a data policy).

The `Policies` screen on the Administration panel provides administrators the ability to define custom policies for their SanteDB deployment.

{% hint style="info" %}
Most plugins and solutions will seed data and action policies into the iCDR when installed. This ensures consistent identification between iCDR instances.
{% endhint %}

## Policy List

The policy list shows view of the configured system policies in a particular iCDR instance. The policy list provides basic functionality for managing policies including:

![](<../../../../.gitbook/assets/image (421).png>)

* Creating security and privacy new policies in the iCDR instance
* Deleting non-system policies (system policies cannot be deleted)
* Viewing policies

## Creating Policies

Administrators can create new security and privacy policies in SanteDB by using the `Create` button.

![](<../../../../.gitbook/assets/image (445).png>)

| UUID           | The unique identifier for the policy.                                                                                                                                                                                                                                          |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| OID            | The object identifier for the policy. These must be unique and are inheritable. For example policy `1.2.3.4` is implied to be the parent of policies `1.2.3.4.0` and `1.2.3.4.1`. Granting a role or device `1.2.3.4` grants `1.2.3.4.0` and `1.2.3.4.1`.                      |
| Name           | A short, descriptive name for the policy.                                                                                                                                                                                                                                      |
| C# Handler     | If the policy uses custom enforcement logic, this is the logic which is called when the policy is violated or grant is denied. (implements `IPolicyHandler` , see : [Documentation](http://santesuite.org/assets/doc/net/html/T\_SanteDB\_Core\_Security\_IPolicyHandler.htm)) |
| Allow Override | When enabled, indicates that when the policy is decided as DENY, the result should be an ELEVATE, allowing users with appropriate elevation permission to re-authenticate themselves and override the policy decision (break the glass)                                        |

