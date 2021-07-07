# TEST: SECURITY-PA-04

## References

* [Policy Administration](../../../../../operations/host-administration/santedb-icdr-admin-console/policy-administration.md)

## Discussion

This is a basic test to demonstrate that the Admin Console commands operate correctly when assigning policies to a role.

## Pre-Conditions / Setup

Should have the iCDR administrative console open and logged in successfully.

## Actions/Steps

1- Use the "**policy.assign**" command followed by "**-r" \(**or **"--role"\)** followed ****by the role\(s\) to assign the policy to followed by "**-p**" \(or "**--policy**"\) followed by the policy\(ies\) to apply followed by "**-e**" \(or "**--rule**"\) followed by the action to take \(0/deny, 1/elevate, 2/grant\).

{% hint style="info" %}
If you don't specify the action to take \("e" or "--rule" parameter\) then the default action would be "deny".
{% endhint %}



