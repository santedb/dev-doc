---
description: Testing the successful unlocking a locked application.
---

# TEST: SECURITY-AM-03

## References

* [Application Management](../../../../../../../operations-1/system-administration/security-administration/application-management.md)

## Discussion

This is a basic test to demonstrate that the UI components appear and operate correctly when unlocking a locked application.

## Pre-Conditions / Setup

1. User must be logged into an account with policies granted for unlocking applications.
2. Navigate to **Administration Panel / Security / Applications / List**.

## Actions/Steps

1- Click the **Unlock** button

![](<../../../../../../../.gitbook/assets/10 (3).jpg>)

2- Click  **Ok** to confirm the unlock.

![](<../../../../../../../.gitbook/assets/12 (1).jpg>)

## Expected Behaviour

1- Should display a message asking to confirm the unlock.

![](../../../../../../../.gitbook/assets/11.jpg)

2- Should appear the Status of the application changed to Active.

![](<../../../../../../../.gitbook/assets/13 (1).jpg>)
