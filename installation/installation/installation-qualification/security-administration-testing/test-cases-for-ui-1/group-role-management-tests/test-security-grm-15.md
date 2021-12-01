---
description: Testing successful un-deletion of a group that has previously been deleted.
---

# TEST: SECURITY-GRM-04

## References

* [Group / Role Management](../../../../../../operations-1/system-administration/security-administration/group-role-management.md)
* [TEST: SECURITY-GRM-03](test-security-grm-03-1.md)

## Discussion

After a group record has been deleted, it is not permanently destroyed. Deleted groups can be **Un-Deleted** and is recovered from a Status of Obsolete in so doing.&#x20;

## Pre-Conditions / Setup

1\. Follow the instructions from [TEST: SECURITY-GRM-03](test-security-grm-03-1.md) to delete a group (e.g. "Muddsville").

## Actions/Steps

&#x20;1\. While the **Show Deleted** button is toggled (darkened), deleted groups can be un-deleted by clicking the **Un-Delete** button corresponding to the group to be recovered.

![](<../../../../../../.gitbook/assets/image (311).png>)

2\. Click the **OK** button on the confirmation prompt appearing in the browser.

![](<../../../../../../.gitbook/assets/image (291).png>)

## Expected Behaviour

* Table is reloaded to show deleted groups and should no longer include the group that was just reactivated (e.g. "Muddsville").

![](<../../../../../../.gitbook/assets/image (335).png>)

* After toggling back to the un-deleted groups, the reactivated group should appear there.

![](<../../../../../../.gitbook/assets/image (310).png>)
