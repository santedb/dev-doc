# Policy Administration

You can use the iCDR administrative console to list policies and assign policies to objects within the iCDR instance. Creating new policies needs to be done through the UI. For more information visit [Security Policy Management](../../security-administration/security-policy-management.md).

### Viewing Policies

You can view all security policies configured on the server using the "**policy.list**" command, specifying optional filter parameters.

```text
> policy.list
SID                                    Name                                   Oid                                       
a14d0096-d62a-11eb-8248-00155d640b09   Create-Policy-Test                     1.3.6.1.4.1.3349.3.1.5.9.2.99.4           
57a36a62-d5c5-11eb-8248-00155d640b09   Access HIV ART Number                  1.3.6.1.4.1.3349.3.1.5.9.2.99.2           
62073cae-8c1e-11eb-be65-00155d640b09   Testy Mctesterson                      1.3.6.1.4.1.66666.3.1.5.9.2.0.14          
598c0e00-82fb-11eb-8dcd-0242ac130007   Read PubSub Subscriptions              1.3.6.1.4.1.33349.3.1.5.9.2.0.14.4        
598c0e00-82fb-11eb-8dcd-0242ac130006   Delete PubSub Subscriptions            1.3.6.1.4.1.33349.3.1.5.9.2.0.14.3        
```

The optional filter parameters for policy.list are.

| Parameter | Description | Example |
| :--- | :--- | :--- |
| -n | List policies with specified name | policy.list -n test |
| -o | List policies with specified OID pattern | policy.list -o 1.3.6.1.4.1.33349 |

## Assigning Policies

You can assign security policies to devices, roles, and/or applications by using "**policy.assign**" command,  followed by specifying parameters.

| Parameter | Description |
| :--- | :--- |
| -r or --role | The role\(s\) to assign the policy to |
| -a or --application | The application\(s\) to assign the policy to |
| -d or --device | The device\(s\) to assign the policy to |
| -e or --rule | The action to take \(0/deny, 1/elevate, 2/grant\) |
| -p or --policy | The policy\(ies\) to apply |

{% hint style="info" %}
The object parameter \( role or application or device \) is required. 

The policy parameter is required.

The action parameter \("-r" or "--rule"\) specifies the action to take and by default is set to 0 \(Deny\) if is not specified.
{% endhint %}

**Example:**

```text
> policy.assign -a Create-Application-Test -e 2 -p 1.3.6.1.4.1.33349.3.1.5.9.2.999
Grant: Override Disclosure TO Create-Application-Test
>
```

```text
> policy.assign -a Create-Application-Test -p 1.3.6.1.4.1.33349.3.1.5.9.2.999
Deny: Override Disclosure TO Create-Application-Test
>
```

