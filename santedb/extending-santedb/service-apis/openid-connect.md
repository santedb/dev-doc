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

![](../../../.gitbook/assets/image%20%28154%29.png)

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

![](../../../.gitbook/assets/image%20%28155%29.png)

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

![](../../../.gitbook/assets/image%20%28152%29.png)

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

![](../../../.gitbook/assets/image%20%28156%29.png)

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



