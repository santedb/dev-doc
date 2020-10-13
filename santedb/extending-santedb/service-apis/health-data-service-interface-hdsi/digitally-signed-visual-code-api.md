# Digitally Signed Visual Code API

SanteDB provides two special services which can be used to generate digitally signed visual codes. These codes can then be used by the resolution APIs to directly link to a discrete record on the SanteDB iCDR or dCDR services.

The two services which are leveraged to generate a digitally signed pointer are:

* IBarcodeGeneratorService - Used to generate the PNG image which represents the visual code pointing at a record, and
* IResourcePointerService - Used to generate the digitally signed payload of the visual code.

## Service API

There are three APIs which are exposed on the HDSI which should be used for generating and/or resolving resources.

* /{resource}/\_code/{authority} - Returns the visual code as configured by the dCDR or iCDR interface \(as configured by the system\)
* /{resource}/\_ptr - Returns the output of the IResourcePointerService \(by default JWS\) so the consumer of the API can generate an appropriate visual code and/or send the signed payload directly to another solution.
* /\_ptr - Allows the a consumer to send a generated resource pointer to the API and have the API redirect the caller to the appropriate resource.

### \_ptr Operation

The generation of a resource pointer and the visual code are both retrieved using simple HTTP GET operations. The \_ptr operation uses the HTTP SEARCH operation, a request for this operation would be:

```javascript
SEARCH http://example.com/hdsi/_ptr
Content-Type: application/x-www-form-urlencoded

code=JWS_PAYLOAD_HERE
```

Upon successful location of the resource, the iCDR or dCDR will return an HTTP 303 result

```javascript
HTTP/1.1 303 See Other
Location: http://example.com/hdsi/Patient/{uuid}/_history/{uuid}
```

It is expected that callers will use the HTTP GET to GET the resulting location from the iCDR or dCDR server.

## Visual Code Specification 

The default visual code generator in SanteDB iCDR and dCDR is a structured QR code containing an RFC7515 payload. A sample of a resource pointer code is:

![](../../../../.gitbook/assets/image%20%28163%29.png)

The code is comprised of a header, payload and signature. The IBarcodeGeneratorService is responsible for the generation of this visual format \(in this case a QR code\) while the IResourcePointerService \(in this case the JWS resource pointer\) generates the payload.

### Visual Code Header

The decoded header for such a visual resource pointer code is illustrated below:

```javascript
{
  "alg": "HS256",
  "typ": "x-santedb+Entity",
  "key": "jwsdefault"
}
```

#### ALG Header

The algorithm used to sign the visual code is the ALG header. The two supported configurations for this header in SanteDB are:

* HS256 -&gt; HMAC signature based on a shared secret key between the generator and the reader.
* RS256 -&gt; Uses RSA encryption to encrypt the SHA256 generated hash of the payload. The generator uses a private key to encrypt the payload hash, whilst the reader uses a public key to decrypt and verify the hash.

The algorithm header in SanteDB is dictated by the type of key used to sign the payload. SanteDB will not permit the use of any hashing algorithm. The algorithm configured for the specified KEY header must be used.

#### TYP Header

The content type header \(TYP\) uses the extended mime type of x-santedb+TYPE. This indicates the type of data that is being pointed at in the payload. The pointer can reference any known type in SanteDB, commonly used are:

| Content Type | Resource Type |
| :--- | :--- |
| x-santedb+Entity | Indicates the visual code points to an Entity \(unspecified type\) |
| x-santedb+Act | Indicates the visual code points to an Act \(unspecified type\) |
| x-santedb+Patient | Indicates the visual code points to a Patient |
| x-santedb+Material | Code points to a Material or Manufactured Material \(such as substance, equipment, etc.\) |
| x-santedb+Place | Code points to a location such as a Hospital, Clinic, Village, Region, District, etc. |

#### KEY Header

The key header indicates the configured key to be used for validating the authenticity of the code \(the key which was used to sign the data\). In SanteDB's iCDR and dCDR the key identifiers are configured in the primary configuration file in the `SecurityConfigurationSection` section in the signingKeys section. 

This key can be any key configured in SanteDB, however two common key identifiers used are either:

* JWSDefault -&gt; The default JWS signing key which can be either an x.509 certificate \(in which case RSA signatures are used\) or an HMAC plaintext secret.
* SA.UUID -&gt; The configured private key of the device which generated the key. This is the configured ApplicationSecret in SanteDB for that application.

### Visual Code Payload

The payload of the resource pointer JWS content is a structured JSON file \(unencrypted\) which contains **only the identifiers** for the resource which the object points at. No other contextual or sensitive information is provided. An example of the payload is:

```javascript
{
  "iat": 1602023055,
  "id": [
    {
      "value": "490005410588",
      "ns": "MOHS_GEN_NHID"
    }
  ]
}
```

This minimal payload is used on purpose to ensure:

1. Any reader can easily read the contents of the pointer without disclosing sensitive identifying information about what the code means.
2. Authentication is required to query the iCDR or dCDR to obtain full context of the code.
3. Authorization is applied on querying the iCDR or dCDR to ensure that appropriate privacy controls are enforced.



