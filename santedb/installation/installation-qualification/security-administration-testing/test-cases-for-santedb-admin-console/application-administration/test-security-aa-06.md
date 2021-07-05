# TEST: SECURITY-AA-06

## References

* [Application Administration](./)

## Discussion

This is a basic test to demonstrate that the Admin Console commands operate correctly when undeleting a deleted application.

## Pre-Conditions / Setup

Should have the iCDR administrative console open and logged in successfully.

## Actions/Steps

1- Use "**application.undel**" command followed by the name of the application you wish to undelete.

```text
> application.undel Create-Application-Test
```

2- **Test Validation**: Use "**application.list**" command .\(This command lists all the applications\)

## Expected Behaviour

1- Should 

```text
> application.undel Create-Applicat
```

2- Should the deleted application \("Create-Application-Test"\) reappear on the list of applications.

```text
> application.list
SID                                    Name                     Last Auth.             Lockout                ILA  A
ebb1fb1a-d8d1-11eb-8249-00155d640b09   test2                                                                  0    *
e30f0976-d8d1-11eb-8249-00155d640b09   test                                                                   0    *
a01a3472-d36f-11eb-8248-00155d640b09   Create-Application-Test                                                0    *
```

