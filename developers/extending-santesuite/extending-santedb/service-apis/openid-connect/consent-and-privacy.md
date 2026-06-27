# Consent & Privacy

The SanteDB software solution implements a policy enforcement scheme similar to the XACML architectural components (see: [privacy-architecture.md](../../../../../santedb/privacy-architecture.md "mention")).&#x20;

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

When an elevation condition is detected, the server will respond with a 401 Unauthorized response.&#x20;

For example:

```http
HTTP/1.1 401 Unauthorized
WWW-Authenticate: Bearer realm="elbonia.santesuite.net" 
     error="insufficient_scope" 
     scope="1.3.6.1.4.1.33349.3.1.5.9.3" 
     error_description="Policy Restricted Information / Confidential (1.3.6.1.4.1.33349.3.1.5.9.3) was violated by 'fujiman' with outcome 'Elevate'"


```

When this condition occurs, clients may use the Override headers as discussed in the [OpenID Connect ](./#client-claims)page.

#### Masked Results

Depending on the configuration of the SanteDB server, requesting access to a protected record may implement masking logic rather than returning a 401. This provides an opportunity for clients to discover that a privacy protection has occurred.&#x20;

For example, when fetching a FHIR patient resource for a protected patient, the response may disclose a masked record, as illustrated below

```json
{
  "resourceType": "Patient",
  "id": "e73ae3fe-dc6d-4e05-a5da-715f90f5c789",
  "meta": {
    "versionId": "78b88d73-4fc2-403a-836a-425e445a7fab",
    "lastUpdated": "0001-01-01T00:00:00-08:00",
    "security": [
      {
        "system": "http://santedb.org/security/policy",
        "code": "1.3.6.1.4.1.33349.3.1.5.9.3",
        "display": "Restricted Information / Confidential"
      }
    ],
    "tag": [
      {
        "system": "http://santedb.org/fhir/tags",
        "code": "$pep.masked:true"
      }
    ]
  },
  "text": {
    "status": "generated",
    "div": ""
  },
  "active": true,
  "name": [
    {
      "use": "anonymous"
    }
  ]
}
```

The same pattern applies using the HDSI interface. Th masking is indicated by the tag `$pep.masked` and the `security` labels applied indicate the policies which are applied to the object.

### Break-The-Glass (BTG) / Consent Override Authentication

Upon receiving the `401` unauthorized response from a resource or detecting a masked record, the client is expected to prompt for the user's credentials (or collect a new auth code from the OAUTH endpoint) and explicitly override the identified policies.<br>

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

The client is expected to pass the following client assertions to the iCDR or dCDR instance:

| Assertion                                      | Value                                                                                                                                                          |
| ---------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `urn:oasis:names:tc:xspa:1.0:subject:facility` | The UUID of the facility in which the user is accessing the record                                                                                             |
| `urn:santedb:org:claim:override`               | The fixed value `true`                                                                                                                                         |
| `urn:oasis:names:tc:xacml:2.0:action:purpose`  | The purpose of accession of the record / override. This should be the UUID of the appropriate concept, or the mnemonic (example: `Purpose-EmergencyTreatment`) |
| `urn:santedb:org:claim:temporary`              | `true` if the access token is a one-time use (limited to 2 minute), or `false` if the token is expected to be used more than once.                             |

The client assertions are passed via the `X-SanteDB-ClientClaim` header or as a JWT assertion in the `client_assertion` fields in the OAUTH body.
