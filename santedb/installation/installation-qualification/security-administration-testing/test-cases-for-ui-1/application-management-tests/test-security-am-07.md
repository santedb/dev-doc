---
description: >-
  Testing the unsuccessful creation of a new policy when Name and Software Name
  fields are missing.
---

# TEST: SECURITY-AM-07

## References

* [Application Management](../../../../../operations/security-administration/application-management.md)

## Discussion

This is a basic test to demonstrate that the UI components appear and operate correctly when creating a new application leaving the Name and Software Name fields blank.



## **Pre-Conditions / Setup**

1. User must be logged into an account with policies granted for creating applications.
2. Navigate to **Administration Panel / Security / Applications / List**.

## Actions/Steps

1- Click the **Create** button

![](../../../../../../.gitbook/assets/1%20%289%29.jpg)

2- Leave Name and Software Name fields blank and click the **Save** button.\( Name and Software Name fields are required fields \) 

![](../../../../../../.gitbook/assets/3%20%2814%29.jpg)

1- Should navigate to the new Create Application page.

![](../../../../../../.gitbook/assets/2%20%285%29.jpg)

2- Should show an error message below Name field and Software Name field indicating that required field is missing.

