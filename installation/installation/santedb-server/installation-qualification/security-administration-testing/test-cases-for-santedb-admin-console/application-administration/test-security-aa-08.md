---
description: Testing the successful listing of all locked security applications.
---

# TEST: SECURITY-AA-08

## References

* [Application Administration](./)

## Discussion

This is a basic test to demonstrate that the Admin Console commands operate correctly when listing all locked security applications in the SanteDB instance.

## Pre-Conditions / Setup

Should have the iCDR administrative console open and logged in successfully.

## Actions/Steps

1- Use "**application.list**" command followed by "**-l**"  parameter.

```
> application.list -l
```

## Expected Behaviour

&#x20;1- Should display the list of all "locked" security applications in the SanteDB instance .

### _**This page needs to update after the bug issue is resolved.**_
