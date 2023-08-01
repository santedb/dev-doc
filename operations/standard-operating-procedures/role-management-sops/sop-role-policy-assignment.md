# SOP: Role Policy Assignment

## Summary

Whenever a role needs to be granted (or denied) permission to perform an action, access data, or use fields the policy decision point will use the policies assigned to the active roles to determine appropriate action.

### Use Procedure When

* [ ] There is a new policy which needs to be granted or denied from an existing group
* [ ] There is a formal request to block types of data or actions from members of an existing group
* [ ] The legislative or policy environment has changed and policies on roles need to be modified.

## Procedure

### Before Beginning

* [ ] Ensure that the policy and role assignment are documented in a knowledgebase
* [ ] Ensure that the policy has been created&#x20;
* [ ] Ensure that the administrative design matches the desired policy assignment (i.e. should this really be an assignment to an existing group, or should it be an assignment to a new group)&#x20;
* [ ] Familiarize yourself with the [security-architecture.md](../../../santedb/security-architecture.md "mention")
* [ ] Your account has the **Alter Role** security permission

### Procedures / Tasks

1. Access the SanteDB Administrative Portal by[logging-in.md](../../cdr-administration/santedb-administration-panel/logging-in.md "mention")
2. Access the [security-administration](../../cdr-administration/santedb-administration-panel/security-administration/ "mention") menu item
3. Access the [#group-list](../../cdr-administration/santedb-administration-panel/security-administration/managing-groups.md#group-list "mention")
4. Locate the group to which the policies are being assigned/removed and click `Edit`&#x20;
5. Locate the policy (documented in [#assigning-policies](../../cdr-administration/santedb-administration-panel/security-administration/managing-groups.md#assigning-policies "mention")) and press the `Add` button
6. Search for the assigned policy
7. Select the appropriate enforcement permission:
   1. **Grant** - Members of the group should be allowed to access data tagged with the policy or perform actions demanding the policy
   2. **Deny** - Members of the group should not be allowed to access data tagged with the policy or perform actions demanding the policy
   3. **Elevate** - Members of the group may access data or perform actions tagged with the policy, however only after re-authenticating themselves.

### After Completion

* [ ] Close the ticket which was create to assign the policy
* [ ] Notify the manager / most responsible person for the group that the assignment has been changed.

## Summary Information

**Current Status:** Example\
**Reviewed By:** SanteSuite Team

### **Revision History**

<table><thead><tr><th width="150">Author</th><th width="245">Date</th><th>Changes</th></tr></thead><tbody><tr><td>Justin Fyfe (SanteSuite)</td><td>2022-03-15</td><td>Initial Version</td></tr><tr><td></td><td></td><td></td></tr><tr><td></td><td></td><td></td></tr></tbody></table>

### See Also

{% content-ref url="../../../santedb/security-architecture.md" %}
[security-architecture.md](../../../santedb/security-architecture.md)
{% endcontent-ref %}

{% content-ref url="../../../santedb/privacy-architecture.md" %}
[privacy-architecture.md](../../../santedb/privacy-architecture.md)
{% endcontent-ref %}

{% content-ref url="../../cdr-administration/santedb-administration-panel/security-administration/managing-policies.md" %}
[managing-policies.md](../../cdr-administration/santedb-administration-panel/security-administration/managing-policies.md)
{% endcontent-ref %}

{% content-ref url="../../cdr-administration/santedb-administration-panel/security-administration/managing-groups.md" %}
[managing-groups.md](../../cdr-administration/santedb-administration-panel/security-administration/managing-groups.md)
{% endcontent-ref %}

