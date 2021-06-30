# Group / Role Management

Users may be placed into one or more groups in the SanteDB system . A group \(or role\) represents a functional responsibility that a user has plays within the system. For example, you may create a security group for CLINICAL\_STAFF, and another group for HIV\_PHYSICIANS. You can then assign policies to each group.

## Reviewing Groups

Groups can be reviewed by selecting the Security &gt; Group panel on the SanteDB administration panel.

![](../../../../.gitbook/assets/image%20%2830%29.png)

## Creating / Managing Groups

Once you've created a group, you cannot change its name, only its description can be modified in the settings. Unlike users, SecurityRole \(groups\) objects do not have a clinical representation.

### Policies & Permissions

SanteDB supports a very robust policy infrastructure. The security architecture is described more in the architecture section however, in brief policies are applied to users , using applications, on devices. User policy associations occur through  the SecurityRole objects to which the user belongs.

![](../../../../.gitbook/assets/image%20%28131%29.png)

You can set one of three permissions on each policy:

* **Grant:** The user is granted access to the policy \(either permission policy or data policy\) 
* **Deny:**The user is explicitly denied access to the policy \(any permission which demands it, or any data which has it assigned\)
* **Elevate:** By default, the user is denied access to the action/data the policy is attached to , however if the user belongs to a group which has the **Override** policy, they will have the opportunity to elevate themselves \(similar to Windows UAC\) to obtain access to the data or action they were attempting to access.

{% hint style="info" %}
Remember, SanteDB uses the MOST RESTRICTIVE permission for a policy. If a user is a member of two groups, and one group GRANT access to the policy, and another DENY it, the ACL is DENY.
{% endhint %}

To assign a new policy to a group, search for the policy and press the add button, then assign the permission you'd like that group to have.

![](../../../../.gitbook/assets/image%20%2825%29.png)

### Managing Users in Groups

Managing user memberships in a group is done the same was as managing policies. You can add or remove users to/from a group using the Members portion of the edit group panel

![](../../../../.gitbook/assets/image%20%2898%29.png)



