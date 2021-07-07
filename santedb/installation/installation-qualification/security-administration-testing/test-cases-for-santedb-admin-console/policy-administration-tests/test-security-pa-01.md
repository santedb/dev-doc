# TEST: SECURITY-PA-01

## References

* [Policy Administration](../../../../../operations/host-administration/santedb-icdr-admin-console/policy-administration.md)

## Discussion

This is a basic test to demonstrate that the Admin Console commands operate correctly when listing security policies.

## Pre-Conditions / Setup

Should have the iCDR administrative console open and logged in successfully.

## Actions/Steps

1- Use "**policy.list**" command.

```text
> policy.list
```

## Expected Behaviour

1- Should display the list of all security policies configured on the server.

```text
> policy.list
SID                                    Name                                   Oid                                       
a14d0096-d62a-11eb-8248-00155d640b09   Create-Policy-Test                     1.3.6.1.4.1.3349.3.1.5.9.2.99.4           
57a36a62-d5c5-11eb-8248-00155d640b09   Access HIV ART Number                  1.3.6.1.4.1.3349.3.1.5.9.2.99.2           
62073cae-8c1e-11eb-be65-00155d640b09   Testy Mctesterson                      1.3.6.1.4.1.66666.3.1.5.9.2.0.14          
598c0e00-82fb-11eb-8dcd-0242ac130007   Read PubSub Subscriptions              1.3.6.1.4.1.33349.3.1.5.9.2.0.14.4        
598c0e00-82fb-11eb-8dcd-0242ac130006   Delete PubSub Subscriptions            1.3.6.1.4.1.33349.3.1.5.9.2.0.14.3        
598c0e00-82fb-11eb-8dcd-0242ac130005   Disable/Enable PubSub Subscriptions    1.3.6.1.4.1.33349.3.1.5.9.2.0.14.2        
598c0e00-82fb-11eb-8dcd-0242ac130004   Create/Alter PubSub Subscriptions      1.3.6.1.4.1.33349.3.1.5.9.2.0.14.1        
598c0e00-82fb-11eb-8dcd-0242ac130003   Unrestricted PubSub Administration     1.3.6.1.4.1.33349.3.1.5.9.2.0.14          
f45b96ff-646c-4c00-9a58-ea09eee67dad   Alter Local Users                      1.3.6.1.4.1.33349.3.1.5.9.2.0.8.1         
f45b96fe-646c-4c00-9a58-ea09eee67dad   Create Local Users                     1.3.6.1.4.1.33349.3.1.5.9.2.0.4.1         
f45b96ab-646c-4c00-9a58-ea09eee67dad   Allow Impersonation of Application     1.3.6.1.4.1.33349.3.1.5.9.2.1.0.2         
678aa7a0-c177-11ea-9f72-00155d640b09   SUPER SECRET DISCLOSURE                2.25.3049340304933                        
852c7891-c094-11ea-9f6f-00155d640b09   OAUTH Password Reset grant (extende... 1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0.4       
852c7890-c094-11ea-9f6f-00155d640b09   OAUTH authoization code grant flow ... 1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0.3       
852c788e-c094-11ea-9f6f-00155d640b09   OAUTH client_credentials flow permi... 1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0.1       
852c788f-c094-11ea-9f6f-00155d640b09   OAUTH password flow permission         1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0.2       
852c788d-c094-11ea-9f6f-00155d640b09   OAUTH Login                            1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0         
852c785e-c094-11ea-9f6f-00155d640b09   Unrestricted MDM                       1.3.6.1.4.1.33349.3.1.5.9.2.6             
852c7861-c094-11ea-9f6f-00155d640b09   Merge MDM Master                       1.3.6.1.4.1.33349.3.1.5.9.2.6.3           
852c7860-c094-11ea-9f6f-00155d640b09   Read MDM Locals                        1.3.6.1.4.1.33349.3.1.5.9.2.6.2           
852c785f-c094-11ea-9f6f-00155d640b09   Write MDM Master                       1.3.6.1.4.1.33349.3.1.5.9.2.6.1           
e15b96ab-646c-4c00-9a58-ea09eee67dae   Special Security Elevation             1.3.6.1.4.1.33349.3.1.5.9.2.600           
e15b96ab-646c-4c00-9a58-ea09eee67daf   Change Security Challenge Question     1.3.6.1.4.1.33349.3.1.5.9.2.600.1         
e15b96ab-646c-4c00-9a58-ea09eee67dad   Login for Password Reassignment        1.3.6.1.4.1.33349.3.1.5.9.2.1.0.1         
baa227aa-224d-4859-81b3-c1eb2750068f   Administer Applets                     1.3.6.1.4.1.33349.3.1.5.9.2.0.12          
baa227aa-224d-4859-81b3-c1eb275006af   Elevate Clinical Data                  1.3.6.1.4.1.33349.3.1.5.9.2.2.5           
baa227aa-224d-4859-81b3-c1eb2750069f   Assign Policy                          1.3.6.1.4.1.33349.3.1.5.9.2.0.13          
baa227aa-224d-4859-81b3-c1eb2750067f   Access Audit Log                       1.3.6.1.4.1.33349.3.1.5.9.2.0.11          
4a8642cb-28e4-4e9e-bd7b-d6df72b729b2   Query Warehouse Data                   1.3.6.1.4.1.33349.3.1.5.9.2.5.3           
36f1ed35-552e-421a-8f59-629561ab9eb6   Restricted Information                 1.3.6.1.4.1.33349.3.1.5.9.3               
baa124aa-224d-4859-81b3-c1eb2750067e   Write Materials                        1.3.6.1.4.1.33349.3.1.5.9.2.4.1.0         
baa125aa-224d-4859-81b3-c1eb2750067e   Delete Materials                       1.3.6.1.4.1.33349.3.1.5.9.2.4.1.1         
baa126aa-224d-4859-81b3-c1eb2750067e   Read Materials                         1.3.6.1.4.1.33349.3.1.5.9.2.4.0.1.2       
da73c05a-3159-48c8-bbcb-741911d91cd2   Unrestricted All                       1.3.6.1.4.1.33349.3.1.5.9.2               
baa224aa-224d-4859-81b3-c1eb2750067e   Write Places & Orgs                    1.3.6.1.4.1.33349.3.1.5.9.2.4.2.0         
baa225aa-224d-4859-81b3-c1eb2750067e   Delete Places & Orgs                   1.3.6.1.4.1.33349.3.1.5.9.2.4.2.1         
baa226aa-224d-4859-81b3-c1eb2750067e   Read Places & Orgs                     1.3.6.1.4.1.33349.3.1.5.9.2.4.0.2.2       
baa227aa-224d-4859-81b3-c1eb2750067e   Query Places & Orgs                    1.3.6.1.4.1.33349.3.1.5.9.2.4.0.2.3       
baa127aa-224d-4859-81b3-c1eb2750067e   Query Materials                        1.3.6.1.4.1.33349.3.1.5.9.2.4.0.1.3       
ea73c05a-3159-48c8-bbcb-741911d91cd2   Unrestricted Administrative Function   1.3.6.1.4.1.33349.3.1.5.9.2.0             
d80ac1cf-3d6e-429f-a4a0-88c0bbbc839d   Change Password                        1.3.6.1.4.1.33349.3.1.5.9.2.0.1           
9c0d65ac-613e-4a67-8bc6-5ce2c0b42160   Create Role                            1.3.6.1.4.1.33349.3.1.5.9.2.0.2           
79bcc227-0d13-4fbf-a83e-f2b9fce34151   Alter Role                             1.3.6.1.4.1.33349.3.1.5.9.2.0.3           
ab8642cb-28e4-4e9e-bd7b-d6dc72b729b2   Create Identity                        1.3.6.1.4.1.33349.3.1.5.9.2.0.4           
bb8642cb-28e4-4e9e-bd7b-d6dc72b729b2   Create Device                          1.3.6.1.4.1.33349.3.1.5.9.2.0.5           
cb8642cb-28e4-4e9e-bd7b-d6dc72b729b2   Create Application                     1.3.6.1.4.1.33349.3.1.5.9.2.0.6           
db8642cb-28e4-4e9e-bd7b-d6dc72b729b2   Administer Concept Dictionary          1.3.6.1.4.1.33349.3.1.5.9.2.0.7           
eb8642cb-28e4-4e9e-bd7b-d6dc72b729b2   Alter Identity                         1.3.6.1.4.1.33349.3.1.5.9.2.0.8           
fb8642cb-28e4-4e9e-bd7b-d6dc72b729b2   Alter Policy                           1.3.6.1.4.1.33349.3.1.5.9.2.0.9           
fa8642cb-28e4-4e9e-bd7b-d6dc72b729b2   Administer Data Warehouse              1.3.6.1.4.1.33349.3.1.5.9.2.0.10          
d15b96ab-646c-4c00-9a58-ea09eee67d7c   Login                                  1.3.6.1.4.1.33349.3.1.5.9.2.1             
e15b96ab-646c-4c00-9a58-ea09eee67d7c   Login as a Service                     1.3.6.1.4.1.33349.3.1.5.9.2.1.0           
f6840336-4e20-4bc0-b965-baa6d7c80be3   Unrestricted Clinical Data             1.3.6.1.4.1.33349.3.1.5.9.2.2             
b81daf47-17a5-465e-a5fd-706b168b0265   Query Clinical Data                    1.3.6.1.4.1.33349.3.1.5.9.2.2.0           
d7276921-a078-4348-95f2-ed3cde83e607   Write Clinical Data                    1.3.6.1.4.1.33349.3.1.5.9.2.2.1           
2e027dee-ede4-4731-b7fa-cb67ae0586be   Delete Clinical Data                   1.3.6.1.4.1.33349.3.1.5.9.2.2.2           
5fb731bf-4e59-4863-80bd-51757d58ea3b   Read Clinical Data                     1.3.6.1.4.1.33349.3.1.5.9.2.2.3           
5fb731bf-4e59-4863-80bd-51757d58ea9a   Export Clinical Data                   1.3.6.1.4.1.33349.3.1.5.9.2.2.4           
dea891aa-224d-4859-81b3-c1eb2750067e   Override Disclosure                    1.3.6.1.4.1.33349.3.1.5.9.2.999           
eea891aa-224d-4859-81b3-c1eb2750067e   Unrestricted Metadata                  1.3.6.1.4.1.33349.3.1.5.9.2.4             
fea891aa-224d-4859-81b3-c1eb2750067e   Read Metadata                          1.3.6.1.4.1.33349.3.1.5.9.2.4.0           
0ea891aa-224d-4859-81b3-c1eb2750067e   Access Client Administrative Function  1.3.6.1.4.1.33349.3.1.5.9.2.10            
0a8642cb-28e4-4e9e-bd7b-d6df72b729b2   Unrestricted Data Warehouse            1.3.6.1.4.1.33349.3.1.5.9.2.5             
1a8642cb-28e4-4e9e-bd7b-d6df72b729b2   Write Warehouse Data                   1.3.6.1.4.1.33349.3.1.5.9.2.5.0           
2a8642cb-28e4-4e9e-bd7b-d6df72b729b2   Delete Warehouse Data                  1.3.6.1.4.1.33349.3.1.5.9.2.5.1           
3a8642cb-28e4-4e9e-bd7b-d6df72b729b2   Read Warehouse Data                    1.3.6.1.4.1.33349.3.1.5.9.2.5.2           
>

```

