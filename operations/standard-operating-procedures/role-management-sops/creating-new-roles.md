# SOP: Creating New Roles

## Summary

This procedure should be used when a new classification of user within the SanteDB system (an access role) is desired. Access roles are used to control which system functions and data access is granted or denied to a user.

### Use Procedure When

* [ ] A new user classification is required
* [ ] An existing group does not (or can not) fulfill the same purpose
* [ ] When further, restrictive control is required for individual user accounts

## Procedure

### Before Beginning

* [ ] Approvals to create a new role gathered
* [ ] Role has been documented and initial members list established
* [ ] Familiarize yourself with the [security-architecture.md](../../../santedb/security-architecture.md "mention")
* [ ] Your user account has the **Create Roles** policy granted
* [ ] Necessary, context specific approvals and conventions
  * [ ] Include things like signatures required
  * [ ] Or whether the incident needs to be documented
  * [ ] Your IT department should have common security practices in place

### Procedures / Tasks

1. Access the SanteDB Administrative Portal by[logging-in.md](../../cdr-administration/santedb-administration-panel/logging-in.md "mention")
2. Access the [security-administration](../../cdr-administration/santedb-administration-panel/security-administration/ "mention") menu item
3. Access the [#group-list](../../cdr-administration/santedb-administration-panel/security-administration/managing-groups.md#group-list "mention") by clicking groups clicking `Create`
4. Create the group as documented in [#creating-groups](../../cdr-administration/santedb-administration-panel/security-administration/managing-groups.md#creating-groups "mention")
   1. The name of the group should comply to conventions
   2. The name should be unique within the organization/project
5. Assign the appropriate access policies to match documented group function (as documented in [#assigning-policies](../../cdr-administration/santedb-administration-panel/security-administration/managing-groups.md#assigning-policies "mention"))
6. Assign the desired role membership (those for which appropriate documentation has been gathered) . (see: [#assigning-users](../../cdr-administration/santedb-administration-panel/security-administration/managing-groups.md#assigning-users "mention"))

### After Completion

* [ ] Notify the requestor and group members of their access&#x20;
* [ ] Close work item in ticketing system (or related documentation for completion)

## Summary Information

**Current Status:** Sample\
**Reviewed By:** SanteSuite Team

### **Revision History**

<table><thead><tr><th width="150">Author</th><th>Date</th><th>Changes</th></tr></thead><tbody><tr><td>Justin Fyfe (SanteSuite)</td><td>2022-03-15</td><td>Initial Version</td></tr><tr><td></td><td></td><td></td></tr><tr><td></td><td></td><td></td></tr></tbody></table>

### See Also

{% content-ref url="../../cdr-administration/santedb-administration-panel/security-administration/managing-groups.md" %}
[managing-groups.md](../../cdr-administration/santedb-administration-panel/security-administration/managing-groups.md)
{% endcontent-ref %}

{% content-ref url="../../cdr-administration/santedb-icdr-admin-console/group-role-management.md" %}
[group-role-management.md](../../cdr-administration/santedb-icdr-admin-console/group-role-management.md)
{% endcontent-ref %}

