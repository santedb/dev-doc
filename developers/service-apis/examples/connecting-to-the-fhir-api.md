# Connecting to the FHIR API

{% hint style="info" %}
Prior to connecting to any API, your administrator should setup an Application identity and a Device identity (if not using two-way TLS).
{% endhint %}

Note: You should complete the [Obtaining A Session](obtaining-a-session.md) example prior to using this tutorial.

## Getting Conformance Statement

SanteDB iCDR servers can operate in a multitude of roles, as such, some FHIR resources your application uses may have been disabled by the administrator. It is a good practice to obtain the FHIR conformance statement prior to executing operations against the FHIR server. This is done by:

```http
OPTIONS http://mpi-test.local:8080/fhir HTTP/1.1
User-Agent: Fiddler
Host: mpi-test.local:8080
```

The response of this will be a FHIR CapabilityStatement in XML:

```http
HTTP/1.1 200 OK
Content-Length: 14950
Content-Type: application/fhir+xml
Content-Location: http://mpi-test.local:8080/fhirmetadata
Last-Modified: Mon, 11 Jan 2021 12:22:08 GMT
Server: Microsoft-HTTPAPI/2.0
X-PoweredBy: SanteDB v2.0.60.25971 (Montreal)
X-GeneratedOn: 2021-01-11T12:22:09.2795003-05:00
Access-Control-Allow-Origin: *
Access-Control-Allow-Methods: OPTIONS,POST,PUT,PATCH,DELETE,GET
Access-Control-Allow-Headers: Content-Type,Accept-Encoding,Content-Encoding
Date: Mon, 11 Jan 2021 17:22:09 GMT

<?xml version="1.0"?>
<CapabilityStatement xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://hl7.org/fhir">
  <text>
    <status value="generated" />
```

You can verify that the appropriate operations and appropriate resources are supported by the particular iCDR server deployment.

### Requesting JSON Responses

You can request a JSON payload by appending the `Accept: application/fhir+json` to your request.

```http
OPTIONS http://mpi-test.local:8080/fhir HTTP/1.1
User-Agent: Fiddler
Host: mpi-test.local:8080
Accept: application/fhir+json
```

Which results in a JSON return:

```http
HTTP/1.1 200 OK
Content-Length: 8410
Content-Type: application/fhir+json
Content-Location: http://mpi-test.local:8080/fhirmetadata
Server: Microsoft-HTTPAPI/2.0
X-PoweredBy: SanteDB v2.0.60.25971 (Montreal)
X-GeneratedOn: 2021-01-11T12:24:07.0378833-05:00
Access-Control-Allow-Origin: *
Access-Control-Allow-Methods: OPTIONS,POST,PUT,PATCH,DELETE,GET
Access-Control-Allow-Headers: Content-Type,Accept-Encoding,Content-Encoding
Date: Mon, 11 Jan 2021 17:24:07 GMT

{"resourceType":"CapabilityStatement",
```

## Searching Data

You can locate data on the FHIR service by executing the appropriate GET operation against the requested resource, for example, to find a patient who presents an identifier of 799229340878 you could execute the following query:

```http
GET http://mpi-test.local:8080/fhir/Patient?identifier=799229340878 HTTP/1.1
User-Agent: Fiddler
Host: mpi-test.local:8080
Accept: application/fhir+json
Authorization: bearer E878ABAE3054EB11AFFD00155D640B2349E9BDE39EBC9082EE1D45358EC838D18122DF3FC1EFE649858826108F5881C6
```

Which will return the structured data for that patient in a FHIR Bundle:

```http
HTTP/1.1 200 OK
Content-Length: 3733
Content-Type: application/fhir+json
Last-Modified: Mon, 11 Jan 2021 12:28:55 GMT
Server: Microsoft-HTTPAPI/2.0
X-PoweredBy: SanteDB v2.0.60.25971 (Montreal)
X-GeneratedOn: 2021-01-11T12:28:56.0462209-05:00
Access-Control-Allow-Origin: *
Access-Control-Allow-Methods: OPTIONS,POST,PUT,PATCH,DELETE,GET
Access-Control-Allow-Headers: Content-Type,Accept-Encoding,Content-Encoding
Date: Mon, 11 Jan 2021 17:28:56 GMT

{"resourceType...
```

## Submitting Data

To submit data, you should create an HTTP POST (to create a new resource) or PUT (to update an existing resource) to the appropriate URI defined by the FHIR standard. For example, to create a new patient John Test&#x20;

```http
POST http://mpi-test.local:8080/fhir/Patient?identifier=799229340878 HTTP/1.1
User-Agent: Fiddler
Host: mpi-test.local:8080
Accept: application/fhir+json
Authorization: bearer 5E52AE073554EB11BF1600155D640B23E0DB71384E69B27B015D257B2F6975C2CABA85ADE4A4B49E5D6D9ACBC688DF1B
Content-Type: application/fhir+json
Content-Length: 675

{
    "resourceType": "Patient",
    "identifier": [
        {
            "system": "http://test.com/domain",
            "value": "4323423342"
        }
    ],
    "active": true,
    "name": [
        {
            "given": ["John"],
            "family": ["Test"]
        }
    ],
    "gender": "male",
    "birthDate": "1985-03-02",
    "address":
        [
            {
                "line": ["321 Street Address"],
                "state": "Ontario"
            }
        ]
}
```

This will create a new patient and return the created data:

```http
HTTP/1.1 201 Created
Content-Length: 2770
Content-Type: application/fhir+json
Content-Location: http://mempi-test.local:8080/fhir/Patient/f41833f0-5620-472e-bd6f-29d2cbb65a59/_history/
Last-Modified: Mon, 11 Jan 2021 12:48:40 GMT
ETag: W/""
Server: Microsoft-HTTPAPI/2.0
X-PoweredBy: SanteDB v2.0.60.25971 (Montreal)
X-GeneratedOn: 2021-01-11T12:48:42.2124309-05:00
Access-Control-Allow-Origin: *
Access-Control-Allow-Methods: OPTIONS,POST,PUT,PATCH,DELETE,GET
Access-Control-Allow-Headers: Content-Type,Accept-Encoding,Content-Encoding
Date: Mon, 11 Jan 2021 17:48:42 GMT

{"resourceType":"Patient ...
```

### MDM Master

If you're running the iCDR in MDM mode, the returned resource will be the generated LOCAL record for this patient. The iCDR will generate a MASTER record which expressed in the refer link:

```javascript
"link": [{
        "other": {
            "reference": "http://mpi-test.local:8080/fhir/Patient/8b554b4e-f0e1-42ec-85b7-296d521dd71b/_history/861b20d1-992d-487a-8788-63fae840f6bd", 
            "display": "[Patient]"
        },
        "type": "refer"
    }]
```

The MASTER can be retrieved by following this link. You may wish to do this to:

* Retrieve generated data (such as a national health identifier)
* Obtain data from other records the iCDR has matched (other candidate locals)
