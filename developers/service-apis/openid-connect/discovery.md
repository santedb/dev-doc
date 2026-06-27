# Discovery

The discovery URL for OpenID Connect is located at the `{base}/auth/well-known/openid-configuration` endpoint. The discovery endpoint contains:

* Configured locations of each open-id service
* Configured policy scopes (see: [policy-information-provider-pip.md](../../server-plugins/implementing-.net-features/service-definitions/policy-information-provider-pip.md "mention"))
* Configured grant types

An example of requesting the discovery document is shown below:

```http
HTTP/1.1 200 OK
Server: nginx/1.24.0 (Ubuntu)
Date: Sat, 27 Jun 2026 18:36:27 GMT
Content-Type: application/json
Content-Length: 4920
Connection: keep-alive

{
  "issuer": "https://ims-ncc1701.santesuite.net",
  "authorization_endpoint": "https://ims-ncc1701.santesuite.net:8443/auth/authorize",
  "token_endpoint": "https://ims-ncc1701.santesuite.net:8443/auth/oauth2_token",
  "userinfo_endpoint": "https://ims-ncc1701.santesuite.net:8443/auth/userinfo",
  "jwks_uri": "https://ims-ncc1701.santesuite.net:8443/auth/jwks",
  "scopes_supported": [
    // Truncated
  ],
  "response_types_supported": [
    "code"
  ],
  "grant_types_supported": [
    "authorization_code",
    "client_credentials",
    "x_challenge",
    "password",
    "refresh_token",
    "x-refresh-cookie"
  ],
  "subject_types_supported": [
    "public"
  ],
  "id_token_signing_alg_values_supported": [
    "RS256"
  ],
  "end_session_endpoint": "https://ims-ncc1701.santesuite.net:8443/auth/signout"
}
```

### Configuration Settings

The discovery document generated is controlled via a series of configuration settings in the SanteDB iCDR or dCDR configuration file.&#x20;

| Configuration Setting                                | OpenID Connect Document                                                                              |
| ---------------------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| /OAuthConfigurationSection/@issuerName               | `issuer`                                                                                             |
| /RestConfigurationSection/baseAddress                | `authorization_endpoint`, `token_endpoint`, `userinfo_endpoint`, `end_session_endpoint`,  `jwks_url` |
| /SecurityConfigurationSection/signingkeys/jwsdefault | `id_token_signing_alg_values_supported`                                                              |
