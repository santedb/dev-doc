# Client Assertions

SanteDB's OpenID connect provides an extended header option which can be used by clients to append claims about the user they would like reflected in the session. The authentication server will validate these claims against the authenticated principal and may return either an HTTP 200 (authentication success) or an HTTP 400 (authentication fail).

Client claims are passed via the X-SanteDBClient-Claim header as a semi-colon separated base64 enoded list. For example, this particular series of claims indicates the user is breaking the glass because of emergency access.&#x20;

```
X-SanteDBClient-Claim: (b64)PolicyOverride=1;PurposeOfUse=EMERG
```

The types of claims which may be sent to the OpenID Connect service are listed below:

| Claim                 | Description                                                                                                                                                                                               | Example                |
| --------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------- |
| PolicyOverride        | When true or 1, indicates that the user is re-authenticating for the purpose of violating/bypassing a policy.                                                                                             | 1                      |
| PurposeOfUse          | The codified purposes of use, the reason why the policy override is being executed.                                                                                                                       | <p>EMERG</p><p>PAT</p> |
| ResourceId            | When specified, indicates the UUID of a specific resource for which the user is overriding the policy system.                                                                                             | UUID                   |
| SubjectRole           | The role which the user is playing (if the user plays multiple roles). For example, if a user is both a Physician and a Surgeon they may specify which role they are authenticating as.                   |                        |
| SubjectOrganizationID | The organization within which the user is authenticating themselves. For example, if a user works both at Good Health Hospital and Health Clinic Inc. this would allow specification of the organization. |                        |
| Language              | If the user wishes to switch messages from the server to a different language, the language of messages being returned from the server.                                                                   | en, fr                 |

When performing a consent override, you may also specify the policies which are being overridden in the source scope property. For example, the Elbonia MPI defines a directive "SUPER SECRET DISCLOSURE" , if the user Allison wished to override the default consent decision, the client could send a password grant illustrated below:

```http
POST http://mpi-test.local:8080/auth/oauth2_token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
X-Device-Authorization: BASIC RGVidWdlZS1FMEQ1NUVBNUQ2Q0Q6MCpTdV8yfk9kSjdAR2NjNw==
X-SanteDBClient-Claim: PolicyOverride=1;PurposeOfUse=EMERG
Host: mpi-test.local:8080
Content-Length: 112

grant_type=password&scope=2.25.3049340304933&username=allison&password=Mohawk123&client_id=fiddler&client_secret=fiddler
```

{% hint style="info" %}
SanteDB will support the use of `client_assertion_type` and `client_assertion` in future releases.
{% endhint %}
