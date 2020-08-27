# OpenID Connect

SanteDB supports OpenID Connect on the https://servername:8443/auth endpoint. 

## Discovery / Configuration

The configuration of the SanteDB server can be obtained via a GET to the openid-configuration endpoint, as illustrated below.

```text
GET http://mpi-test.local:8080/auth/.well-known/openid-configuration HTTP/1.1
Host: mpi-test.local:8080
```

This results in an OpenID configuration response, illustrated in below.

```text
HTTP/1.1 200 OK
Content-Length: 2382
Content-Type: application/json
Server: Microsoft-HTTPAPI/2.0
Date: Tue, 04 Aug 2020 17:19:37 GMT

{
    "issuer": "http://mpi-test.local:8080/auth",
    "authorization_endpoint": "http://mpi-test.local:8080/auth/authorize/",
    "token_endpoint": "http://mpi-test.local:8080/auth/oauth2_token",
    "userinfo_endpoint": "http://mpi-test.local:8080/auth/userinfo",
    "jwks_uri": "http://mpi-test.local:8080/auth/jwks",
    "scopes_supported": ["1.3.6.1.4.1.33349.3.1.5.9.2", ... ],
    "response_types_supported": ["code"],
    "grant_types_supported": ["client_credentials", "password", "authorization_code"],
    "subject_types_supported": ["public"],
    "id_token_signing_alg_values_supported": ["HS256"]
}
```

For more information see [OpenID Connect Discovery](https://openid.net/specs/openid-connect-discovery-1_0.html) documentation.

## Grant Types

SanteDB supports four different grant types described in this session. The grant types and flows are not described here. For a good reference on OpenID Connect flows see [RFC67849](https://tools.ietf.org/html/rfc6749#section-1.3).

You can limit the types of grants each device, application, and security role are allowed to authenticate by denying the following policies on those objects:

| Policy | Grant | Description |
| :--- | :--- | :--- |
| OAUTH Login \(1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0\) | Any | When denied, the specified object cannot authenticate using OAUTH or OpenID Connect. |
| OAUTH password flow \(1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0.2\) | Password | When denied, the specified object is prohibited from using the password grant flow. |
| OAUTH client\_credentials flow \(1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0.1\) | Client Credentials | When denied, the specified object is prohibited from using the client\_credentials grant flow. |
| OAUTH authorization code flow \(1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0.3\) | Authorization Code | When denied, the specified object is prohibited from using the authorization\_code grant flow. |
| OAUTH password reset flow \(1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0.4\) | x\_challenge | When denied, the specified object is prohibited from using the extended TFA challenge authentication for password resets. |

### Password Grant

The password grant is a grant whereby a trusted user agent \(mobile app, website, etc.\) collects both the username and password for the user which are then sent to the IdP server.

This grant is useful for:

* Authenticating users from an offline application context \(periodic authentication where the UA collects passwords anyways\)
* Authenticating users from a first party application or trusted application

![](../../../../.gitbook/assets/image%20%28154%29.png)

The process is as follows:

1. User Agent uses OIDC discovery to determine appropriate scopes, grants, and configuration of the remote target.
2. User agent collects username and password \(not specified how\)
3. User agent requests an access token from the IdP
4. The IdP responds with an id\_token, auth\_token, refresh\_token for subsequent use.
5. The user agent continues to access the protected resource.

The request for a token using the password is illustrated below:

```text
POST http://mpi-test.local:8080/auth/oauth2_token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: mpi-test.local:8080
Content-Length: 146

grant_type=password&username=user&password=@Pass123&scope=*&client_id=mymobileapp&client_secret=secret
```

The server responds with a token response \(documented below\).

### Client Credentials Grant

The client credentials grant creates an application principal based on the device/application pair presented on the authentication request.

This grant is useful for:

* A background task from a trusted application on a trusted device \(like synchronization\)
* HIE traffic between nodes / applications where dual-PKI infrastructure is prohibitively complex.

![](../../../../.gitbook/assets/image%20%28155%29.png)

The process for this is:

1. User agent runs a discovery request \(optional\)
2. User agent sends a token request \(client\_credentials grant\)
3. User agent receives an application authentication token
4. User agent accesses the resource

A client credentials grant is illustrated below:

```text
POST http://mpi-test.local:8080/auth/oauth2_token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
X-Device-Authorization: BASIC RGVidWdlZS1FMEQ1NUVBNUQ2Q0Q6MCpTdV8yfk9kSjdAR2NjNw==
Host: mpi-test.local:8080
Content-Length: 112

grant_type=client_credentials&scope=*&client_id=myMobileApp&client_secret=myAppSecret
```

SanteDB's IdP mandates that application principals can only be created if the device is known. The device identity can be established from client-certificates \(if configured\), or in a simpler deployment, using the device's identifier and secret in the X-Device-Authorization header.

### Authorization Code Grant

The authorization code grant is a traditional OpenID connect grant flow you've probably seen used online. The authorization code grant does not expose the user name or password to the client application. Rather, the user is redirected to the SanteDB IdP server where their credentials are collected by SanteDB and the resulting authorization code is sent back to the UA.

This grant is helpful when:

* Integrating third party applications where you may or may not trust the application 
* SSO where you wish to use cookies to auto-login users.

![](../../../../.gitbook/assets/image%20%28152%29.png)

The process for this is:

1. User is directed to the login screen on SanteDB's IdP \(established from OIDC discovery\)
2. User enters their username and password into the IdP
3. IdP generates an authorization code and redirects the user's browser back to the application requesting the token
4. Application uses the authorization code provided to exchange for auth tokens
5. IdP validates the authorization code and responds with token.
6. Application accesses the protected resource.

In this flow the first step is a redirection to the IdP supplying the minimum parameters:

```text
GET http://server:8080/auth/authorize/index.html?redirect_uri=http://myapp.com&client_id=fiddler&scope=openid&response_type=code&response_mode=query&state=1234
```

The parameters for this initial request are: 

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Values</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">redirect_uri</td>
      <td style="text-align:left">The URI where the IdP should redirect the user&apos;s browser</td>
      <td
      style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">client_id</td>
      <td style="text-align:left">
        <p>The client identification of the requestor (note: must have grant</p>
        <p>to do authorization code flow)</p>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">scope</td>
      <td style="text-align:left">The scope of the grant . Must contain openid, optionally can
        <br />contain additional policies being requested)</td>
      <td style="text-align:left">openid</td>
    </tr>
    <tr>
      <td style="text-align:left">claim</td>
      <td style="text-align:left">Claims made about the user separated</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">state</td>
      <td style="text-align:left">A unique state identifier which can be used to maintain
        <br />state across requests</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">response_type</td>
      <td style="text-align:left">
        <p>The type of response being asked for.</p>
        <p>code =&gt; The redirect is supplied a code which can be exchanged</p>
        <p>token =&gt;</p>
      </td>
      <td style="text-align:left">code or token</td>
    </tr>
    <tr>
      <td style="text-align:left">response_mode</td>
      <td style="text-align:left">
        <p>The mode of response.</p>
        <p>query =&gt; The redirect will be made via a GET operation with the
          <br
          />authorization code being the supplied as a query parameter.</p>
        <p>post =&gt; The redirect will be made via a POST operation with the authorization
          code being supplied as a form parameter.</p>
      </td>
      <td style="text-align:left">form_post or query</td>
    </tr>
    <tr>
      <td style="text-align:left">nonce</td>
      <td style="text-align:left">A unique NONCE which is passed back to the requestor to ensure tampering
        has not occurred.</td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

The user will be presented with the defined IdP login screen \(specified in the applets manifest\).

![](../../../../.gitbook/assets/image%20%28156%29.png)

If successful, the browser will be redirected back to the caller. 

When an response\_type = code and response\_mode = query, a simple redirect is performed 

```text
HTTP/1.1 302 Found
Content-Length: 0
Location: http://myapp.com/auth_back?code=907...8D808&state=1234
Server: Microsoft-HTTPAPI/2.0
Date: Tue, 04 Aug 2020 18:16:10 GMT
```

When response\_type = code and response\_mode = form\_post, a form post is returned

```text
HTTP/1.1 200 OK
Content-Length: 584
Content-Type: text/html
Server: Microsoft-HTTPAPI/2.0
Date: Tue, 04 Aug 2020 18:27:42 GMT

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
    <body onload="javascript:document.forms[0].submit()">
        <form method="POST" action="http://localhost">
            <input type="hidden" name="code" value="kKrL...YCA" />
            <input type="hidden" name="state" value="1234" />
            <button type="submit">Complete Authentication</button>
        </form>
    </body>
</html>
```

If using response\_type = token and response\_mode = form\_post, a form post with an auth token is directly sent back to the UA for use with the assigned resource. This may be disabled based on your configuration.

```text
HTTP/1.1 200 OK
Content-Length: 538
Content-Type: text/html
Server: Microsoft-HTTPAPI/2.0
Date: Tue, 04 Aug 2020 18:33:15 GMT

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
    <body onload="javascript:document.forms[0].submit()">
        <form method="POST" action="http://localhost">
            <input type="hidden" name="access_token" value="D8A29CF...17335628" />
            <input type="hidden" name="state" value="1234" />
            <button type="submit">Complete Authentication</button>
        </form>
    </body>
</html>
```

## Identity Token Contents

The id\_token of the OpenID connect token response contains a series of claims about the user, device and application used to authenticate the user. The identity token is in the JWT token \([jwt.io](https://jwt.io)\). The token, when processed contains claims similar to those shown below:

```text
{
  "unique_name": "demoadmin",
  "role": "ADMINISTRATORS",
  "authmethod": "Password",
  "nameid": "2a348c6e-c158-11ea-9f6f-00155d640b09",
  "actort": "33932b42-6f4b-4659-8849-6aca54139d8e",
  "email": "administrator@santesuite.net",
  "appid": "54558ca5-c093-11ea-9f6f-00155d640b09",
  "scope": [
    "1.3.6.1.4.1.33349.3.1.5.9.2.0",
    "1.3.6.1.4.1.33349.3.1.5.9.2.1",
    "1.3.6.1.4.1.33349.3.1.5.9.2.10",
    "1.3.6.1.4.1.33349.3.1.5.9.2.4",
    "1.3.6.1.4.1.33349.3.1.5.9.2.6",
    "1.3.6.1.4.1.33349.3.1.5.9.2.2"
  ],
  "jti": "D4BE3C469CE8EA11A4D800155D640B09B936F76D94711250935D5ECFD214D9372552A891B010C8470602D9E56D351D7E",
  "iat": "1598556847.8982",
  "exp": 1598558647,
  "sub": "2a348c6e-c158-11ea-9f6f-00155d640b09",
  "iss": "https://elbonia.santesuite.net:8443/auth",
  "nbf": 1598556847
}
```

The claims provided by the identity provider are:

| Claim | Description | Example |
| :--- | :--- | :--- |
| unique\_name | The user name of the user, application or device which has been authenticated. | demoadmin |
| role | The role\(s\) to which the user belongs. | ADMINISTRATORS |
| authmethod | The grant flow which resulted in the identity token being generated. | Password |
| nameid | The SID of the user for which the token was generated. | UUID |
| actort | Identifies the classification of the actor \(human, system, etc.\) |  |
| email | The primary e-mail address for use for security correspondence of the user. |  |
| appid | The SID of the application which is granted use of the application |  |
| scope | The policies which the current session token has been granted by the IDP. See: [Consent and Privacy](consent-and-privacy.md) |  |
| jti | The unique identifier of the session from the issuer. |  |
| iat | Issued at |  |
| exp | Expiration time |  |
| sub | The primary subject of the session. Note: This may be a user's SID \(if the session is a password grant\) or an application SID \(if the session is a client\_credentials grant\). |  |
| iss | The issuer of the token. |  |
| nbf | The effective time of the session. |  |

## Client Claims

SanteDB's OpenID connect provides an extended header option which can be used by clients to append claims about the user they would like reflected in the session. The authentication server will validate these claims against the authenticated principal and may return either an HTTP 200 \(authentication success\) or an HTTP 400 \(authentication fail\).

Client claims are passed via the X-SanteDBClient-Claim header. For example, this particular series of claims indicates the user is breaking the glass because of emergency access.

```text
X-SanteDBClient-Claim: PolicyOverride=1;PurposeOfUse=EMERG
```

The types of claims which may be sent to the OpenID Connect service are listed below:

<table>
  <thead>
    <tr>
      <th style="text-align:left">Claim</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Example</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">PolicyOverride</td>
      <td style="text-align:left">When true or 1, indicates that the user is re-authenticating for the purpose
        of violating/bypassing a policy.</td>
      <td style="text-align:left">1</td>
    </tr>
    <tr>
      <td style="text-align:left">PurposeOfUse</td>
      <td style="text-align:left">The codified purposes of use, the reason why the policy override is being
        executed.</td>
      <td style="text-align:left">
        <p>EMERG</p>
        <p>PAT</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">ResourceId</td>
      <td style="text-align:left">When specified, indicates the UUID of a specific resource for which the
        user is overriding the policy system.</td>
      <td style="text-align:left">UUID</td>
    </tr>
    <tr>
      <td style="text-align:left">SubjectRole</td>
      <td style="text-align:left">The role which the user is playing (if the user plays multiple roles).
        For example, if a user is both a Physician and a Surgeon they may specify
        which role they are authenticating as.</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">SubjectOrganizationID</td>
      <td style="text-align:left">The organization within which the user is authenticating themselves. For
        example, if a user works both at Good Health Hospital and Health Clinic
        Inc. this would allow specification of the organization.</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Language</td>
      <td style="text-align:left">If the user wishes to switch messages from the server to a different language,
        the language of messages being returned from the server.</td>
      <td style="text-align:left">en, fr</td>
    </tr>
  </tbody>
</table>

When performing a consent override, you may also specify the policies which are being overridden in the source scope property. For example, the Elbonia MPI defines a directive "SUPER SECRET DISCLOSURE" , if the user Allison wished to override the default consent decision, the client could send a password grant illustrated below:

```text
POST http://mpi-test.local:8080/auth/oauth2_token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
X-Device-Authorization: BASIC RGVidWdlZS1FMEQ1NUVBNUQ2Q0Q6MCpTdV8yfk9kSjdAR2NjNw==
X-SanteDBClient-Claim: PolicyOverride=1;PurposeOfUse=EMERG
Host: mpi-test.local:8080
Content-Length: 112

grant_type=password&scope=2.25.3049340304933&username=allison&password=Mohawk123&client_id=fiddler&client_secret=fiddler
```

