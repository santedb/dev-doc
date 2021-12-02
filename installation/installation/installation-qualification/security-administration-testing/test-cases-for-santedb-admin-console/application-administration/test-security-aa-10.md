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

1- Use "**application.add**" command followed by a name you wish to give to the new application (for instance "Create-Application-SDBAC") followed by  "**-s**" parameter followed by the secret you want to set.

```
> application.add Create-Application-SDBAC -s TestSecret
```

## Expected Behaviour

1- Should show : "CREATE \<applican name>".

{% hint style="info" %}
In this case the Application Secret is not displayed as usually it is after creating an application since the secret is what we have set after "-s" parameter.
{% endhint %}

```
> application.add Create-Application-SDBAC -s TestSecret
CREATE Create-Application-SDBAC
>
```
