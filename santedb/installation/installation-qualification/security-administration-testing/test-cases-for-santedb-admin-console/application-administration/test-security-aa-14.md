---
description: >-
  Testing the unsuccessful creation of a new application when application name
  parameter missing
---

# TEST: SECURITY-AA-14

## References

* [Application Administration](./)

## Discussion

This is a basic test to demonstrate the Admin Console commands operate correctly when adding a new security application ****without specifying the application name parameter.

## Pre-Conditions / Setup

Should have the iCDR administrative console open and logged in successfully.

## Actions/Steps

1- Use "**application.add**" command.

```text
> application.add
```

## Expected Behaviour

1- Should show : "Application secret: ..." followed by an Error message indicating that name can not be null.

```text
> application.add
Application secret: B30F61126184
ERR: Exception has been thrown by the target of an invocation.
        1:Value cannot be null.
Parameter name: source
>
```

