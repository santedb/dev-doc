# TEST: SECURITY-AA-04

## References

* [Application Administration](./)

## Discussion

This is a basic test to demonstrate that the Admin Console commands operate correctly when unlocking a locked application.

## Pre-Conditions / Setup

Should have the iCDR administrative console open and logged in successfully.

## Actions/Steps

1- Use "**application.lock**" command followed by the name of the application you wish to unlock.

```text
> application.lock Create-Application-Test
```

2- **Test Validation**: Use "**application.info**" command  followed by appliction name.

## Expected Behaviour

1- Should 

```text
> application.lock Create-Application-Test
>
```

2- Should appear the "Lockout" row with no value.

```text
> application.info Create-Application-Test
Name: Create-Application-Test
SID: a01a3472-d36f-11eb-8248-00155d640b09
Invalid Auth:
Lockout:
Last Auth:
Created: 2021-06-22T11:36:34.5714130-04:00 (demoadmin)
Updated: 2021-07-02T14:58:06.4363120-04:00 (Administrator)
        Effective Policies:
```



