# TEST: SECURITY-AM-01

## References

* [Application Management](../../../../operations/security-administration/application-management.md)

## Discussion

This is a basic test to demonstrate that the UI components appear and operate correctly when creating a new application.

## Pre-Conditions / Setup

A user should have been logged in and have the right to create an application.

## Actions/Steps

1- Click the Create button  

![](../../../../../.gitbook/assets/1%20%284%29.jpg)

2- Fill out the fields appropriately and click the Save button. \(keep in mind that  1-Name field is a required field and MUST be filled 2-Sofware Name should be filled too or  there would be a business rule violation error although the application is created anyways \) 

![](../../../../../.gitbook/assets/3%20%287%29.jpg)

## Expected Behaviour

1- Should navigate to the new Create Application page.

![](../../../../../.gitbook/assets/2%20%281%29.jpg)

2-

* Should momentarily display success message in the top right corner
* When navigate to Application Management List page, Should appear New Application\(**Create-Application-Test7**\) **** in the table of applications on the List page with Application Name matching that put in the form required to create a new application.

![](../../../../../.gitbook/assets/4%20%282%29.jpg)

![](../../../../../.gitbook/assets/5.jpg)

