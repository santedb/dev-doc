# Managing Groups

In SanteDB iCDR permits the grouping together of users into logical groups. Security groups are collections of users which have one or more policies associated with them.&#x20;

{% hint style="info" %}
Users which belong to multiple groups follow a most-restrictive policy enforcement scheme. Meaning a user who is a member of `CLINICAL_STAFF` and `ADMINISTRATORS` may effectively have no permissions. Consult the [#most-restrictive-policy-enforcement](../../../../santedb/security-architecture.md#most-restrictive-policy-enforcement "mention")documentation for more information.
{% endhint %}

## Group List

The summary screen for SanteDB groups shows a comprehensive list of all roles registered in the system. The group list provides controls to create, edit and delete groups in the iCDR system.

![](<../../../../.gitbook/assets/image (439) (1) (1) (1).png>)

The are available in the group list screen are:

* Create: Creates a new group
* Show Deleted: Shows the groups which have been previously deleted
* Edit: Edit the indicated group details
* Delete: Deletes the group.

### Deleted Groups

You can use the `Show Deleted` button to list the groups which are not active (i.e. deleted) in the SanteDB system.&#x20;

![](<../../../../.gitbook/assets/image (425).png>)

Pressing the `Un-Delete` button will re-activate the group.&#x20;

{% hint style="info" %}
When a group is deleted, the users within that group will not carry any policies, permissions or attributes from the group.
{% endhint %}

### Danger Zone Groups

There are several groups in SanteDB which are system groups. You can edit these groups and remove them, however doing so may cause system instability in SanteDB. These groups are:

| SYSTEM      | Provides the base level permissions for the SYSTEM account. These are permissions that background processes and daemon services have.           |
| ----------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| ANONYMOUS   | Provides the base level permissions or the ANONYMOUS account. Any user visiting which has not authenticated will have these permissions.        |
| DEVICE      | Provides the base policies which new Security Devices will have when they are created. This is a skeleton policy container for DEVICE accounts. |
| APPLICATION | Provides the base policies which new Security Applications will have.                                                                           |

## Creating Groups

Administrators may wish to create new groups for a variety of reasons. For example:

* To segregate users based on functional role (Data Reviewers, Approvers, Vaccine Managers, etc.)
* To isolate users based on class (Super Users, Power Users, etc.)
* To organize users by department (MRI Technicians, Emergency Room)

When creating a new group, the name and a brief description of the group is required.

![](<../../../../.gitbook/assets/image (423).png>)

## Group Details

When editing a group or after creating a new group, the detail view of the group will be shown.&#x20;

![](<../../../../.gitbook/assets/image (434) (1) (1).png>)

This view shows the basic details of the group, and permits editing of the group name and description, as well as access to the groups security id (SID)

### Assigning Policies

By default a new group will have no policies associated with the group. Administrators should use the `Policies` section to add or alter policies. Policies are added by first searching for the policy and then pressing the `+` button.&#x20;

![](<../../../../.gitbook/assets/image (438) (1) (1).png>)

By default a group will be assigned the policy with a GRANT permission. You can alter these by clicking the permission.

![](<../../../../.gitbook/assets/image (433) (1) (1) (1).png>)

The permission types in SanteDB are:

* Grant - Users in the group will be granted access to any action or data carrying the policy
* Deny - Users in the group are not permitted to access any action or data carrying the policy.
* Elevate - Users in the group are, by default, DENY the request, and the server will send a authentication challenge back to the requestor. Users may be required to provide a reason for override and must provide their password.

Policies can be removed from a group  by clicking the `Remove` button. When a policy is removed, it means that the group has no specific grant applied to the policy (i.e. if the user is in another group its grant will apply, otherwise the default of DENY is applied).

### Assigning Users

Users can be assigned and removed directly from the group using the group detail page. Users are assigned and removed in the `Members` section of the group panel.

![](<../../../../.gitbook/assets/image (424).png>)

Adding users to the group is a similar process as adding policies, the user account is searched and then added to the group using the `+` button.

{% hint style="info" %}
Removing a user from their group does not immediately remove them from the group in their current session. The user's new permission set will apply when the user logs out and logs back into a new session.
{% endhint %}
