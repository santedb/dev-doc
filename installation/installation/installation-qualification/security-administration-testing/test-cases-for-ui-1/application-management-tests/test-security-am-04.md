---
description: Testing the successful deleting an application.
---

# TEST: SECURITY-AM-04

## References

* [Application Management](broken-reference)

## Discussion

This is a basic test to demonstrate that the UI components appear and operate correctly when deleting an existing application.

## Pre-Conditions / Setup

1. User must be logged into an account with policies granted for deleting applications.
2. Navigate to **Administration Panel / Security / Applications / List**



## Actions/Steps

1- Click the **Delete** button

![](<../../../../../../.gitbook/assets/14 (1).jpg>)

2- Click  **Ok** to confirm the delete.

![](<../../../../../../.gitbook/assets/16 (1).jpg>)

## Expected Behaviour

1- Should display a message asking to confirm the delete.

![](<../../../../../../.gitbook/assets/15 (2).jpg>)

2- Deleted application (Create-Application-Test) Should disappear from the Applications/List page.

![](<../../../../../../.gitbook/assets/17 (1).jpg>)
