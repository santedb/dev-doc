---
description: >-
  Testing the successful adding a new security application with setting
  application secret.
---

# TEST: SECURITY-AA-10

## References

* [Application Administration](./)

## Discussion

This is a basic test to demonstrate the Admin Console commands operate correctly when adding a new security application with setting application secret.

## Pre-Conditions / Setup

Should have the iCDR administrative console open and logged in successfully.

## Actions/Steps

1- Use "**application.add**" command followed by a name you wish to give to the new application \(for instance "Application-Create-SDBAC"\) followed by  "**-s**" parameter followed by the secret you want to set.

```text
> application.add Create-Application-SDBAC -s TestSecret
```

## Expected Behaviour

1- Should show : "CREATE &lt;applican name&gt;".

```text
> application.add Create-Application-SDBAC -s TestSecret
CREATE Create-Application-SDBAC
>
```

