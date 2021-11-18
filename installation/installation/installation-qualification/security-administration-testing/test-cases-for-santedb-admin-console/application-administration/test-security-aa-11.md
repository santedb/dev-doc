---
description: >-
  Testing the successful adding a new security application with setting the
  policies to grant the application.
---

# TEST: SECURITY-AA-11

## References

* [Application Administration](./)

## Discussion

This is a basic test to demonstrate the Admin Console commands operate correctly when adding a new security application with setting the policies to grant the application.

## Pre-Conditions / Setup

Should have the iCDR administrative console open and logged in successfully.

## Actions/Steps

1- Use "**application.add**" command followed by a name you wish to give to the new application \(for instance "Create-Application-SDBAC2"\) followed by  "**-g**" parameter followed by the policy OID you want to grant the application.\(for example 1.3.6.1.4.1.33349.3.1.5.9.2.999 \(Override Disclosure\)\)

```text
> application.add Create-Application-SDBAC2 -g 1.3.6.1.4.1.33349.3.1.5.9.2.999
```

2- To test the  validation of the created application with granted policy use "**application.info**" command  followed by the Application Name \(This command displays all the detailed information about an application \)

```text
> application.info Create-Application-SDBAC2
```

## Expected Behaviour

1-  Should show : "Application secret: ..." followed by "CREATE &lt;applican name&gt;".

```text
> application.add Create-Application-SDBAC2 -g 1.3.6.1.4.1.33349.3.1.5.9.2.999
Application secret: 2BEDE80AD320
CREATE Create-Application-SDBAC2
>
```

2- Should the assigned policy \("Override Disclosure"\) appear in the Effective Policies row with action Grant \(Explicit\)

### _**This page needs to update after the bug issue is resolved.**_

