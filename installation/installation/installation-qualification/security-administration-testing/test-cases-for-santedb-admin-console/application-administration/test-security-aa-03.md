---
description: Testing the successful locking a security application.
---

# TEST: SECURITY-AA-03

## References

* [Application Administration](./)

## Discussion

This is a basic test to demonstrate that the Admin Console commands operate correctly when locking an existing application.

## Pre-Conditions / Setup

Should have the iCDR administrative console open and logged in successfully.

## Actions/Steps

1- Use "**appliction**.**lock**" command with a "**-l**" flag, followed by the name of the application you wish to lock.

```
> application.lock -l Create-Application-Test
```

2- **Test Validation**: Use "**application.info**" command  followed by application name.

```
> application.info Create-Application-Test
```

## Expected Behaviour

1- Should&#x20;

```
> application.lock -l Create-Application-Test
>
```

2- Should appear  "Lockout" row with some value.

```
> application.info Create-Application-Test
Name: Create-Application-Test
SID: a01a3472-d36f-11eb-8248-00155d640b09
Invalid Auth:
Lockout: 9999-12-21T18:59:59.9999990-05:00
Last Auth:
Created: 2021-06-22T11:36:34.5714130-04:00 (demoadmin)
Updated: 2021-07-02T14:48:39.9337610-04:00 (Administrator)
        Effective Policies:
```
