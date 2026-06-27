# Identity Token Contents

The id\_token of the OpenID connect token response contains a series of claims about the user, device and application used to authenticate the user. The identity token is in the JWT token ([jwt.io](https://jwt.io)). The token, when processed contains claims similar to those shown below:

```json
{
  "aud": [
    "org.santedb.disconnected_client.www"
  ],
  "iss": "JIMS-IMS-DEV",
  "exp": 1782588724,
  "iat": 1782588125,
  "nbf": 1782588125,
  "extensions": {
      // Truncated
  },
  "sid": "7bab05c0-725d-11f1-83df-b330ccb2d877",
  "scope": [
    // Truncated
  ],
  "name": "fujiman",
  "sub": "3fddb159-621b-4ba8-a585-5396df5abc83",
  "actor": "33932b42-6f4b-4659-8849-6aca54139d8e",
  "role": [
    "USERS",
    "CLINICAL_STAFF",
    "CLINICAL_MANAGERS"
  ],
  "realm": "https://ims-ncc1701.santesuite.net:8443/",
  "at_hash": "g27KA0OAMqtqw66NAdwx1g",
  "jti": "VunVYZ2267v2URhnu3aooA1ZcFA1E9QMGgxw97hO5rk"
}
```

## Extended Claims

Plugins installed on the SanteDB iCDR may add extended claims to the identity token generated. All extended claims are placed in the `extensions` array of the JWT.

### IHE Internet User Assertion (IUA)

The IUA claims are placed in the `ihe_iua` extension and contain:

* The subject person ID (the CDR `Person` record which owns the token)
* The facility(ies) which the subject has logged into
* The full name of the subject
* The purposes of use for the session

The example below shows the contents of the IUA extension for a session which has been elevated.

```json
"extensions": {
    "ihe_iua": {
      "purpose_of_use": [
        {
          "system": "http://santedb.org/conceptset/PurposeOfUse",
          "code": "PurposeOfUse-PatientRequest^http://santedb.org/conceptset/PurposeOfUse"
        },
        {
          "system": "http://santedb.org/conceptset/PurposeOfUse",
          "code": "8b18c2b6-916a-11ea-bb37-0242ac130002^http://santedb.org/conceptset/PurposeOfUse"
        }
      ],
      "subject_facility_id": "774dc415-6bfb-4cf5-a2c4-cca6fa22f3ea",
      "person_id": "f4adcee7-77f3-490b-8f0b-d273d7493462",
      "subject_name": "Manager Mr. Fuji"
    },
  }
```

### SanteDB Extended Claims

SanteDB provides extended claims which allow clients to determine additional information about the holder and the purpose of the session. The example below shows these extended claims:

```json
"santedb": {
      "lang": "en",
      "appid": "48d9d2bb-7f11-4e1e-981e-623cc7f567f8",
      "usrid": "3fddb159-621b-4ba8-a585-5396df5abc83",
      "devid": "142369d0-f1f1-40d8-927b-eeb750eceb3c",
      "isOverride": "true",
      "temporary": "true",
      "appname": "org.santedb.disconnected_client.www"
    }
```

| Claim        | Type    | Value                                                                                                                     |
| ------------ | ------- | ------------------------------------------------------------------------------------------------------------------------- |
| `lang`       | String  | The language of the session (selected by the user at login or the default language for the user account)                  |
| `appid`      | UUID    | The application's SID (the application SID of the `client_id`)                                                            |
| `usrid`      | UUID    | The user's SID                                                                                                            |
| `devid`      | UUID    | The device's SID                                                                                                          |
| `isOverride` | Boolean | When true, indicates that the session is an override (break the glass)                                                    |
| `temporary`  | Boolean | When true indicates that the session is not a standard length session (for password reset, BTG, or shorter access tokens) |
| `appname`    | String  | The application name of the `client_id`                                                                                   |
