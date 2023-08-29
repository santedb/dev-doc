# Visual Resource Pointer API

SanteDB provides two special services which can be used to generate digitally signed visual codes. These codes can then be used by the resolution APIs to directly link to a discrete record on the SanteDB iCDR or dCDR services.

The two services which are leveraged to generate a digitally signed pointer are:

* IBarcodeGeneratorService - Used to generate the PNG image which represents the visual code pointing at a record, and
* IResourcePointerService - Used to generate the digitally signed payload of the visual code.

## Service API

There are three APIs which are exposed on the HDSI which should be used for generating and/or resolving resources.

* /{resource}/\_code/{authority} - Returns the visual code as configured by the dCDR or iCDR interface (as configured by the system)
* /{resource}/\_ptr - Returns the output of the IResourcePointerService (by default JWS) so the consumer of the API can generate an appropriate visual code and/or send the signed payload directly to another solution.
* /\_ptr - Allows the a consumer to send a generated resource pointer to the API and have the API redirect the caller to the appropriate resource.

### \_ptr Operation

The generation of a resource pointer and the visual code are both retrieved using simple HTTP GET operations. The \_ptr operation uses the HTTP SEARCH operation, a request for this operation would be:

```http
SEARCH http://example.com/hdsi/_ptr HTTP/1.1
Content-Type: application/x-www-form-urlencoded

code=JWS_PAYLOAD_HERE
```

Upon successful location of the resource, the iCDR or dCDR will return an HTTP 303 result

```http
HTTP/1.1 303 See Other HTTP/1.1
Location: http://example.com/hdsi/Patient/{uuid}/_history/{uuid}
```

It is expected that callers will use the HTTP GET to GET the resulting location from the iCDR or dCDR server.

{% hint style="info" %}
Visual codes will only ever resolve to a single resource. This means codes which represent multiple patients, substance administrations, locations, materials, etc. are considered invalid by the API and return a 500 error.
{% endhint %}

## Visual Code Specification  (SanteDB 2.x)

The default visual code generator in SanteDB iCDR and dCDR is a structured QR code containing an RFC7515 payload. A sample of a resource pointer code is:

![](<../../../.gitbook/assets/image (163).png>)

The code is comprised of a header, payload and signature. The IBarcodeGeneratorService is responsible for the generation of this visual format (in this case a QR code) while the IResourcePointerService (in this case the JWS resource pointer) generates the payload.

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

* HS256 -> HMAC signature based on a shared secret key between the generator and the reader.
* RS256 -> Uses RSA encryption to encrypt the SHA256 generated hash of the payload. The generator uses a private key to encrypt the payload hash, whilst the reader uses a public key to decrypt and verify the hash.

The algorithm header in SanteDB is dictated by the type of key used to sign the payload. SanteDB will not permit the use of any hashing algorithm, the algorithm specified in the **ALG** header must match the configured algorithm for the key in the **KEY** header.&#x20;

{% hint style="info" %}
When designing your SanteDB solution, it is recommended you do not use jwsdefault key, rather, you should create your own named key and configured the JWS resource pointer to leverage that key. This allows for specifying different keys for different programmes / consumer applications.
{% endhint %}

#### TYP Header

The content type header (TYP) uses the extended mime type of x-santedb+TYPE. This indicates the type of data that is being pointed at in the payload. The pointer can reference any known type in SanteDB, commonly used are:

| Content Type       | Resource Type                                                                           |
| ------------------ | --------------------------------------------------------------------------------------- |
| x-santedb+Entity   | Indicates the visual code points to an Entity (unspecified type)                        |
| x-santedb+Act      | Indicates the visual code points to an Act (unspecified type)                           |
| x-santedb+Patient  | Indicates the visual code points to a Patient                                           |
| x-santedb+Material | Code points to a Material or Manufactured Material (such as substance, equipment, etc.) |
| x-santedb+Place    | Code points to a location such as a Hospital, Clinic, Village, Region, District, etc.   |

#### KEY Header

The key header indicates the configured key to be used for validating the authenticity of the code (the key which was used to sign the data). In SanteDB's iCDR and dCDR the key identifiers are configured in the primary configuration file in the `SecurityConfigurationSection` section in the signingKeys section.&#x20;

This key can be any key configured in SanteDB, however two common key identifiers used are either:

* JWSDefault -> The default JWS signing key which can be either an x.509 certificate (in which case RSA signatures are used) or an HMAC plaintext secret.
* SA.UUID -> The configured private key of the device which generated the key. This is the configured \` in SanteDB for that application.

### Visual Code Payload

The payload of the resource pointer JWS content is a structured JSON file (unencrypted) which contains **only the identifiers** for the resource which the object points at. No other contextual or sensitive information is provided. An example of the payload is:

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

## Visual Code Specification (SanteDB 3.x)

SanteDB 3.0 has been expanded to include searches for different types of barcode information such as [Smart Health Cards (SHC)](https://smarthealth.cards/en/). Because of this the formatting of the VRP barcodes has been changed. The payload still uses JWS and the JWS payload remains the same, however the QR code is encoded with `svrp://HEX_ENCODED_BYTES`. This payload should be sent to the `_ptr` and search operations.

### Visual Code Header

The header of a SanteDB 3.x VRP QR code is identified by the type `application/x.santedb.vrp` in the JWS header.&#x20;

```
{
  "alg": "RS256",
  "typ": "application/x.santedb.vrp",
  "kid": "6DF462EB94ECD87D57B1ECF53CAA436673FA02A4",
  "x5t": "bfRi65Ts2H1Xsez1PKpDZnP6AqQ",
  "zip": "DEF",
  "cty": null
}
```

The following headers are included in a SanteDB VRP:

* alg: Must be either RS256 (if x509 certificates are used - as it the default for QR codes generated from the web clients) or HS256
* typ: Fixed to `application/x.santedb.vrp`
* kid: The named key identifier in the `/.well-known/jwks` endpoint on the SanteDB server (note: this KID is the configured digital signature certificate for the device which generated the code)
* x5t: The key thumbprint
* zip: All VRP codes are compressed with the `deflate` algorithm, indicated by the DEF value in this header.

### Visual Code Payload

The visual resource pointer payload includes metadata about the resource which is being pointed to. The payload is formatted as metadata + resource data:

```
{
  "ver": "3.0.1041.0",
  "iat": 1693325183,
  "sub": "09cd5d98-20d8-40b2-95a0-ad0b209592d1",
  "gen_by": "Administrator",
  "data": {
    "$type": "Patient",
    "identifier": {
      "SLB_MHMS_GEN_MPI_UHID": [
        {
          "value": "XXXXXXXXX874",
          "checkDigit": null
        }
      ]
    }
  }
}
```

* ver: The version of SanteDB which generated the VRP
* iat: The timestamp that the VRP was generated
* sub: The KEY of the resource which the VRP is pointing at
* gen\_by: The user which generated the VRP
* data.$type: The type of data being pointed at
* data.identifier: The identifier of the object being pointed at. Note: That these identifiers are masked on VRPs which point at PHI.
