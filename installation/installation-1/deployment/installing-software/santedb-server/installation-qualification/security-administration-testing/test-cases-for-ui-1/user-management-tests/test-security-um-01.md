---
description: Testing the successful creation of a new user with all properties specified.
---

# TEST: SECURITY-UM-01

## References

* [User Management](broken-reference)

## Discussion

This is a basic test to demonstrate that the UI components appear and operate correctly when creating new users on the [User Management](broken-reference) page.

## Pre-Conditions / Setup

1. User must be logged into an account with policies granted for creating users.
2. Navigate to **Administration Panel / Security / Users / Index**.

{% hint style="info" %}
Each of the tabs below (corresponding to a form section) contain a table that summarizes valid possible values for the form to create a new user.
{% endhint %}

{% tabs %}
{% tab title="Core Properties" %}
| Label        | Value                |
| ------------ | -------------------- |
| **Username** | ClinicalStaffUser123 |
{% endtab %}

{% tab title="Security Properties" %}
| Label                | Value           |
| -------------------- | --------------- |
| **Role**             | CLINICAL\_STAFF |
| **New Password**     | Clinic@l123     |
| **Confirm Password** | Clinic@l123     |
{% endtab %}

{% tab title="Demographic Properties" %}
| Label                  | Value                               |
| ---------------------- | ----------------------------------- |
| **Security E-mail**    | clinical\_staff@user.com            |
| **Security Phone**     | 519-203-8190                        |
| **Given Name**         | John                                |
| **Family Name**        | Doe                                 |
| **Preferred Language** | English                             |
| **Primary Facility**   | Muddy District Distribution Centre  |
| **Employer**           | Muddsville Central Hospital Network |
{% endtab %}
{% endtabs %}

## Actions/Steps

&#x20;   1\. Click the **Create** button to navigate from **Administration Panel / Security / Users / Index** to **Administration Panel / Security / Users / Create User**.

<img src="../../../../../../../../../.gitbook/assets/test1_createButton.png" alt="" data-size="original">&#x20;

&#x20;   2\. Enter valid text into the **Core Properties** drop-down form group.

![](../../../../../../../../../.gitbook/assets/test1\_coreProperties.png)

&#x20;   3\. Enter valid text into the **Security Properties** drop-down form group.

![](../../../../../../../../../.gitbook/assets/test1\_securityProperties.png)

&#x20;   4\. Enter valid text into the **Demographic Properties** drop-down form group.

![](../../../../../../../../../.gitbook/assets/test1\_demographicProperties.png)

&#x20;   5\. Click the **Save** button.

&#x20;   <img src="../../../../../../../../../.gitbook/assets/test1_saveButton (1) (1).png" alt="" data-size="original">&#x20;

## Expected Behaviour

* Automatically navigate to the **Administration Panel / Security / Users / Index** page.
* Momentarily display success message in top right corner: <img src="../../../../../../../../../.gitbook/assets/user_successtoast.png" alt="" data-size="original">&#x20;
* New user (**ClinicalStaffUser123**) should appear in the table of users on the Index page with properties matching those in the "Pre-Conditions / Setup" above.

