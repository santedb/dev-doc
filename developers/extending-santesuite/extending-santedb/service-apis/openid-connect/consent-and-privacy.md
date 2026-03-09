# Consent & Privacy

The SanteDB software solution implements a policy enforcement scheme similar to the XACML architectural components. TODO: Insert link

When accessing resources from the API, a failed consent/policy decision will be provided to the caller.

### Policy Violation - Denied

When a policy violation is denied (the principal does not have any route to elevate), an HTTP 403 Forbidden response is sent with details of the policy violation. For example:

```http
HTTP/1.1 403 Forbidden
Content-Type: application/json

{
    "$type": "PolicyViolationException",
    "message": "Policy '1.3.6.1.4.1.33349.3.1.5.9.2.0.6' was violated by 'Allison' with outcome 'Deny'",
    "policyId": "1.3.6.1.4.1.33349.3.1.5.9.2.0.6",
    "policyOutcome":"Deny",
}
```

### Policy Violation - Elevation

Under certain conditions, some policies which are DENIED can be overridden by the user. The conditions under which this occurs is:

* The policy which was violated has the can override flag set to true
* The user has access to the Override Policy (1.3.6.1.4.1.33349.3.1.5.9.2.999) set to GRANT
* Neither the application, nor the device principal the user is accessing the system with are denied the Override Policy

When an elevation condition is detected, the server will respond with a 401 Unauthorized response. For example:

```http
HTTP/1.1 401 Unauthorized
WWW-Authenticate: Bearer realm="elbonia.santesuite.net" 
     error="insufficient_scope" 
     scope="1.3.6.1.4.1.33349.3.1.5.9.3" 
     error_description="Policy Restricted Information / Confidential (1.3.6.1.4.1.33349.3.1.5.9.3) was violated by 'fujiman' with outcome 'Elevate'"


```

&#x20;When this condition occurs, clients may use the Override headers as discussed in the [OpenID Connect ](./#client-claims)page.

### Break-The-Glass (BTG) / Consent Override Authentication

Upon receiving the `401` unauthorized response from a resource, the client is expected to prompt for the user's credentials (or collect a new auth code from the OAUTH endpoint) and explicitly override the identified policies.<br>

```http
POST /auth/oauth2_token HTTP/1.1
Accept: application/json, text/javascript, */*; q=0.01
Accept-Encoding: gzip, deflate, br, zstd
Content-Type: application/x-www-form-urlencoded
Cookie: _sbr=ZUtoc25RakY5TEJ2U1ZBWkhHczJ1ZE1WejlmS3h4VW1PbllEal9nV1FmQS5MdGFGUkdfeTNYWTFFVzF1a3MzbW81NWgtVUhLUmRlQkpaZGtvVVkyc0lPZ2FremxVNzcwWUU0TjAxVEpmTGlpTFZjZTNYbklCSkUtUDVOWE5jaDJNSHZYc3R3Z3BHNWtrWGp2aDU3YWlIZnprbDRyQzhDc0VZeHp6anQtMVdiNjJHU3Y4b2JULUVSWWEtZ0xMeVdNRlJpWnEyMFFKSW5ac0FWNkp4bHhmdmZIRlktNTBOQ2hUUHdWVXVLc0hxTmRwYnVDRS02R1NLLWlLeUlKS3NKdkxJTjNzVzR1Zlh6WURCcU9rLTZsNjRNclAwX203S2xsWjZmVlE5ZUd3RnZYSmFYM014QTNqcTJ5RHpZLXEzc3R1UUVfUk1nUTZDdmI4NEdmX3p1b0lMa2d4Q3lQVzVKRXZSY25zYU9jU19aZ0x2cHdla3dvY0d5ZXJweHpvTTQyYUE.EBQNzcRhnIDeQsPZbnOwkrlEgyTyID5W6I1cXUs3XSmJIPVs28_dSRoTpdQVOXFh6qw23TyWej1oKEIOdcSoXZqP5PnuJnngW2xwPkW4WqRv0eXbpnRYGOmPlyygl87c59ii5YDvaaFDYtjEvmuryTSr7OAxalvu2OgpzFRXKYNDA0XFkWSfhL0CTU28iW59lkfHs6RrhiSD2lchJ4i7gYjRTX3lfbK0W4ZfcGbhNWkm4ZdClxMRM3nV6AXz5kaXcloRoN5TwHt9ZZE5TPB65V9cOARHUGoJjz2qlyJN3ZHB1UEs39830sBNbzoil-FS9I2oxtPdwz6V-QR1dXTADQ; _sbs=esJyowIc8RGJMxfoiYVNpg.iJAPWmJJPSk2mCC2svL_wC-dq_XF3flVth8jho88c4VsY_vQdCgHG2ye4z_SHSOsyX-pBiMsr2aVTJ0R-P6Ql2YFqgH5TZbvWzAv5jAwnue_imrxSZsIAncHaSH645Pb9lG780RzZTWPFWs5acJQ09Fk0bFDhp8WCTMYlEOV58btP6iIF_6eql18MmKrXpewOVeChMyxmd1oMKJXxzAGyHurTlMGUxj8ym7NIzqzfdjwR8yQVbnzeywoqKcea3gIA8IkBr-9IB5BBCiyC3dTjaJIgDF6QnuL2G76h0j5CBa9ggIKWyaWNZs7a7uhUOgULdtOHMmBf3mtlx30vizxBA
X-SanteDBClient-Claim: dXJuOm9hc2lzOm5hbWVzOnRjOnhzcGE6MS4wOnN1YmplY3Q6ZmFjaWxpdHk9Nzc0ZGM0MTUtNmJmYi00Y2Y1LWEyYzQtY2NhNmZhMjJmM2VhO3VybjpzYW50ZWRiOm9yZzpjbGFpbTpvdmVycmlkZT10cnVlO3VybjpvYXNpczpuYW1lczp0Yzp4YWNtbDoyLjA6YWN0aW9uOnB1cnBvc2U9OGIxOGMyYjYtOTE2YS0xMWVhLWJiMzctMDI0MmFjMTMwMDAyO3VybjpzYW50ZWRiOm9yZzpjbGFpbTp0ZW1wb3Jhcnk9dHJ1ZQ==
X-SdbLanguage: en

grant_type=password&scope=1.3.6.1.4.1.33349.3.1.5.9.3&username=allison&password=Mohawk123&client_id=fiddler&client_secret=fiddler
```
