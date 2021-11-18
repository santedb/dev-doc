---
description: >-
  Testing the successful adding a new security application with a
  description/note to add to the application.
---

# TEST: SECURITY-AA-13

## References

* [Application Administration](./)

## Discussion

This is a basic test to demonstrate the Admin Console commands operate correctly when adding a new security application with a description/note to the application.

## Pre-Conditions / Setup

Should have the iCDR administrative console open and logged in successfully.

## Actions/Steps

1- Use "**application.add**" command followed by a name you wish to give to the new application \(for instance "Application-Create-SDBAC7"\) followed by  "**-n**" parameter followed by the description/note you want to add \(for example: " This is an application created to test the sdbac "\)

```text
> application.add Create-Application-SDBAC7  -n This is an pplication created to test the sdbac
```

## Expected Behaviour

1-  Should show : "Application secret: ..." followed by "CREATE &lt;applican name&gt;".

```text
> application.add Create-Application-SDBAC7  -n This is an pplication created to test the sdbac
Application secret: 84D633E54D12
CREATE Create-Application-SDBAC7
>
```

### _**This page needs to update after the bug issue is resolved.**_

