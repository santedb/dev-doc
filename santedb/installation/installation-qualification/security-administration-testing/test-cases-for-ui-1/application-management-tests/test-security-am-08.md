---
description: >-
  Testing the unsuccessful creation of a new application when using duplicate
  records.
---

# TEST: SECURITY-AM-08

## References

* [Application Management](../../../../../operations/security-administration/application-management.md)

## Discussion

This is a basic test to demonstrate that the UI components appear and operate correctly when creating a new application using duplicate records \(duplicate Name\).



## **Pre-Conditions / Setup**

1. User must be logged into an account with policies granted for creating applications.
2. Navigate to **Administration Panel / Security / Applications / List**.

## Actions/Steps

1- Click the **Create** button.

![](../../../../../../.gitbook/assets/1%20%2814%29.jpg)

 Fill out all the fields appropriately and for the Name field, use a name with which an application exists. \(for example "Create-Application-Test"\)

## Expected Behaviour

1- Should navigate to the new Create Application page.

![](../../../../../../.gitbook/assets/2%20%287%29.jpg)

2- Should show an error message below Name field indicating that duplicate record detected.

![](../../../../../../.gitbook/assets/4%20%287%29.jpg)

