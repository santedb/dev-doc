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
                   scope="2.25.20394393948393" 
                   error_description="Policy 2.25.20394393948393 was violated by 'Allison' with outcome Elevate"
```

&#x20;When this condition occurs, clients may use the Override headers as discussed in the [OpenID Connect ](./#client-claims)page.
