---
description: Patient Merges
---

# TEST: OHIE-CR-08-FHIR

This test ensures that the client registry properly handles merge requests sent by patient identity sources using the PMIR merge mechanism described in IHE Patient Mater Identity Registry.&#x20;

## References

* [Integrating the Health Enterprise Patient Master Identity Registry](https://www.ihe.net/uploadedFiles/Documents/ITI/IHE\_ITI\_Suppl\_PMIR.pdf)
* [HL7 FHIR RelatedPerson Resource](http://hl7.org/fhir/relatedperson.html)
* [HL7 FHIR Patient Resource](http://hl7.org/fhir/patient.html)
* I[ntegrating the Health Enterprise Patient Identity Cross Reference for Mobile](https://www.ihe.net/uploadedFiles/Documents/ITI/IHE\_ITI\_Suppl\_PIXm.pdf)

## Discussion

The PMIR profile makes the assumption that the client is controlling the process of merge by instructing the server to link/de-activate a victim. Since merging is an event which triggers several business rules in the Master Data Management layer, the SanteDB PMIR handler detects this condition (a client attempting to control linking of patients, which is an internal matter) and mimics the equivalent behaviors of `ADT^A40` from HL7v2.&#x20;

Furthermore, the SanteDB implementation of merging behaves as described in `Chapter 3 - Patient Administration` in HL7 Version 2 (see: `3.6.2.1.2`). For example, if two patients from `HOSPITAL_A` are registered as illustrated below (patient 1 with two identifiers and patient 2 with one):

![](<../../../../../.gitbook/assets/image (395).png>)

Then a merge requests where Patient 1 is replaced by Patient 2 would result in a merge such that:

![](<../../../../../.gitbook/assets/image (396).png>)

Subsequent requests to query for a patient using `GREEN_TRIANGLE` would result in `Patient 2` being resolved. This behavior differs from the prescribed behavior of PMIR whereby the victim (in this case Patient 2) is not returned, or continues to be resolved with an inactive flag.

## Pre-Conditions

Prior to running this test ensure that the pre-conditions from [TEST: OHIE-CR-04](test-ohie-cr-04-fhir.md) and [TEST: OHIE-CR-06](test-ohie-cr-06-fhir.md) have been run.

## Authenticate as TEST\_HARNESS

The test harness authenticates against the SanteMPI IdP using a client\_credentials grant for the test-harness-a account.

```http
POST http://localhost:8080/auth/oauth2_token HTTP/1.1
Accept-Encoding: gzip,deflate
Content-Type: application/x-www-form-urlencoded;charset=UTF-8
Content-Length: 87
Host: localhost:8080
Connection: Keep-Alive
User-Agent: Apache-HttpClient/4.5.5 (Java/12.0.1)


grant_type=client_credentials&scope=*&client_secret=TEST_HARNESS&client_id=TEST_HARNESS
```

## Register First Patient Identity in TEST

The test harness sends an authenticated request to create a new patient with a new identifier in TEST domain. Patient details:

* Identifier `FHR-080` in `http://ohie.org/test/test`&#x20;
* Identifier `NID080` in `http://ohie.org/test/nid`&#x20;
* Name: MERGY SMITH
* Gender: Male
* DOB: 1986-05-25

```javascript
{
  "resourceType": "Bundle",
  "type": "message",
  "entry": [
    {
      "fullUrl": "MessageHeader/ohie-cr-08-10-fhir",
      "resource": {
        "resourceType": "MessageHeader",
        "id": "1",
        "eventUri": "urn:ihe:iti:pmir:2019:patient-feed",
        "source": {
          "endpoint": "http://ohie.org/test/test_harness"
        },
        "focus": [
          {
            "reference": "Bundle/ohie-cr-08-10-fhir"
          }
        ],
        "destination": [
          {
            "endpoint": "http://ohie.org/test/endpoint/Bundle"
          }
        ]
      }
    },
    {
      "fullUrl": "http://test.ohie.org/fhir/Bundle/ohie-cr-08-10-fhir",
      "resource": {
        "resourceType": "Bundle",
	   "id": "ohie-cr-08-10-fhir",
        "type": "history",
        "entry": [
          {
         		"fullUrl": "http://test.ohie.org/fhir/Bundle/ohie-cr-08-10-fhir",
			"resource": {
			    "resourceType": "Patient",
			    "id": "ohie-cr-08-10-fhir",
			    "active": true,
			    "identifier": [
			      {
			        "use": "official",
			        "system": "http://ohie.org/test/test",
			        "value": "FHR-080"
			      },
			      {
			        "use":"usual",
			        "system": "http://ohie.org/test/nid",
			        "value":"NID080"
			      }
			    ],
			    "name": [
			      {
			        "use": "official",
			        "family": "SMITH",
			        "given": [
			          "MERGY"
			        ]
			      }
			    ],
			    "gender": "male",
			    "birthDate": "1986-05-25",
			  },
			  "request":{
			  	"method":"PUT",
			  	"url":"Patient/ohie-cr-08-10-fhir"
			  },
			  "response":{
			  	"status":"200"
			  }
			  
          }
        ]
      }
    }
  ]
}
```

### Expected Behaviour

| Requirement | Option    | Description                                                    |
| ----------- | --------- | -------------------------------------------------------------- |
| MUST        | PMIR Only | Return MessageHeader with response.code = ok                   |
| MUST        |           | Return HTTP code of 201 Created                                |
| SHOULD      | PMIR Only | Include an OperationOutcome entry in the response              |
| SHOULD      |           | Include a Patient entry in response containing created patient |
| SHOULD      |           | Include a link to the master identity with code refer          |

## Execute PIXm Query To Validate The First Patient in TEST

The test harness sends an IHE PIXm query for a patient with identifier FHR-080 to the receiver.

```http
GET http://localhost:8080/fhir/Patient/$ihe-pix?sourceIdentifier=http%3A%2F%2Fohie.org%2Ftest%2Ftest%7CFHR-080 HTTP/1.1
Accept-Encoding: gzip,deflate
Authorization: BEARER XXXXXX
Accept: application/fhir+json
Host: localhost:8080
Connection: Keep-Alive
User-Agent: Apache-HttpClient/4.5.5 (Java/12.0.1)

```

### Expected Behaviour

| Requirement | Option | Description                                                                                                                                     |
| ----------- | ------ | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| MUST        |        | Return HTTP code of 200 OK                                                                                                                      |
| MUST        |        | Include a Parameters resource in the response                                                                                                   |
| MUST        |        | <p>Have two parameters carrying the identifier in TEST and NID </p><p>with parameter name of targetIdentifier and values FHR-080 and NID080</p> |
| MUST        |        | <p>Include a parameter with name targetId which has a resource link</p><p>to the created resource from the previous step.</p>                   |

## Register Second Patient Identity in TEST

The test harness sends an authenticated request to create a new patient with a new identifier in TEST domain. Patient details:

* Identifier `FHR-081` in `http://ohie.org/test/test`&#x20;
* Name: MERGY SMYTHE
* Gender: Male
* DOB: 1986-05-25

```javascript
{
  "resourceType": "Bundle",
  "type": "message",
  "entry": [
    {
      "fullUrl": "MessageHeader/ohie-cr-08-10-fhir",
      "resource": {
        "resourceType": "MessageHeader",
        "id": "1",
        "eventUri": "urn:ihe:iti:pmir:2019:patient-feed",
        "source": {
          "endpoint": "http://ohie.org/test/test_harness"
        },
        "focus": [
          {
            "reference": "Bundle/ohie-cr-08-10-fhir"
          }
        ],
        "destination": [
          {
            "endpoint": "http://ohie.org/test/endpoint/Bundle"
          }
        ]
      }
    },
    {
      "fullUrl": "http://test.ohie.org/fhir/Bundle/ohie-cr-08-10-fhir",
      "resource": {
        "resourceType": "Bundle",
	   "id": "ohie-cr-08-10-fhir",
        "type": "history",
        "entry": [
          {
          	"fullUrl": "http://test.ohie.org/fhir/Patient/ohie-cr-08-20-fhir",
          	"resource": {
		    "resourceType": "Patient",
		    "id": "ohie-cr-08-20-fhir",
		    "active": true,
		    "identifier": [
		      {
		        "use": "official",
		        "system": "http://ohie.org/test/test",
		        "value": "FHR-081"
		      }
		    ],
		    "name": [
		      {
		        "use": "official",
		        "family": "SMYTHE",
		        "given": [
		          "MERGY"
		        ]
		      }
		    ],
		    "gender": "male",
		    "birthDate": "1986-05-25",
		  },
			  "request":{
			  	"method":"PUT",
			  	"url":"Patient/ohie-cr-08-20-fhir"
			  },
			  "response":{
			  	"status":"200"
			  }
          }
        ]
      }
    }
  ]
}
```

### Expected Behaviour

| Requirement | Option    | Description                                                    |
| ----------- | --------- | -------------------------------------------------------------- |
| MUST        | PMIR Only | Return MessageHeader with response.code = ok                   |
| MUST        |           | Return HTTP code of 201 Created                                |
| SHOULD      | PMIR Only | Include an OperationOutcome entry in the response              |
| SHOULD      |           | Include a Patient entry in response containing created patient |
| SHOULD      |           | Include a link to the master identity with code refer          |

## Execute PIXm Query To Validate The Second Patient in TEST

The test harness sends an IHE PIXm query for a patient with identifier FHIR-081 to the receiver.

```http
GET http://localhost:8080/fhir/Patient/$ihe-pix?sourceIdentifier=http%3A%2F%2Fohie.org%2Ftest%2Ftest%7CFHR-081 HTTP/1.1
Accept-Encoding: gzip,deflate
Authorization: BEARER XXXXXXX
Accept: application/fhir+json
Host: localhost:8080
Connection: Keep-Alive
User-Agent: Apache-HttpClient/4.5.5 (Java/12.0.1)

```

### Expected Behaviour

| Requirement | Option | Description                                                                                                                   |
| ----------- | ------ | ----------------------------------------------------------------------------------------------------------------------------- |
| MUST        |        | Return HTTP code of 200 OK                                                                                                    |
| MUST        |        | Include a Parameters resource in the response                                                                                 |
| MUST        |        | Have one parameter carrying the identifier in TEST with parameter name of targetIdentifier and value FHR-081.                 |
| MUST        |        | <p>Include a parameter with name targetId which has a resource link</p><p>to the created resource from the previous step.</p> |

## Merge FHR-081 (Patient 2)  into FHR-080 (Patient 1)

In this step the test harness sends a PIMR request to instruct the Client Registry that `FHR-081` has been replaced by `FHR-080`.

```javascript
{
  "resourceType": "Bundle",
  "type": "message",
  "entry": [
    {
      "fullUrl": "MessageHeader/ohie-cr-08-30-fhir",
      "resource": {
        "resourceType": "MessageHeader",
        "id": "1",
        "eventUri": "urn:ihe:iti:pmir:2019:patient-feed",
        "source": {
          "endpoint": "http://ohie.org/test/harness"
        },
        "focus": [
          {
            "reference": "Bundle/ohie-cr-08-30-fhir"
          }
        ],
        "destination": [
          {
            "endpoint": "http://ohie.org/test/endpoint/Bundle"
          }
        ]
      }
    },
    {
      "fullUrl": "http://ohie.org/test/Bundle/ohie-cr-08-30-fhir",
      "resource": {
        "resourceType": "Bundle",
        "id":"ohie-cr-08-30-fhir",
        "type": "history",
        "entry": [
          {
            "fullUrl": "http://ohie.org/test/Patient/ohie-cr-08-30-fhir",
            "resource": {
              "resourceType": "Patient",
              "id": "ohie-cr-08-20-fhir",
              "active": false,
              "identifier": [
                {
                  "use": "official",
                  "system": "http://ohie.org/test/test",
                  "value": "FHR-081"
                }
              ],
              "link": [
                {
                  "other": {
                    "type": "Patient",
                    "identifier": {
                      "value": "FHR-080",
                      "system": "http://ohie.org/test/test"
                    }
                  },
                  "type": "replaced-by"
                }
              ]
            },
            "request": {
              "method": "PUT",
              "url": "Patient/ohie-cr-08-30-fhir"
            },
            "response": {
              "status":"200"
            }
          }
        ]
      }
    }
  ]
}
```

{% hint style="info" %}
You will notice that the `link` element in the above message uses the business identifier reference rather than an absolute reference by URL. This is considered best practice when merging on SanteDB server as it abstracts the logical identifier (which changes as the resource moves between servers). See: [http://hl7.org/fhir/resource.html#identifiers](http://hl7.org/fhir/resource.html#identifiers)
{% endhint %}

| Requirement | Option | Description                                  |
| ----------- | ------ | -------------------------------------------- |
| MUST        |        | Return HTTP code of 200 OK                   |
| MUST        |        | Return MessageHeader with response.code = ok |

### Alternate Merge Request

Alternately, the test harness may fetch/obtain the logical ID of the resource and may indicate the merge using the logical identifier of the resource. For example, if the SanteDB MPI registered a patient with logical identifier `5d0e583f-1fda-4a25-8fbe-f4fb3e876f3c`, the sender may issue a link request such as:

```javascript
"link": [
  {
    "other": {
        "reference": "Patient/5d0e583f-1fda-4a25-8fbe-f4fb3e876f3c"
    },
    "type": "replaced-by"
  }
]
```

### Expected Behavior

| Requirement | Option | Description                                       |
| ----------- | ------ | ------------------------------------------------- |
| MUST        |        | Return MessageHeader with response.code = ok      |
| MUST        |        | Return HTTP code of 200 OK                        |
| SHOULD      |        | Include an OperationOutcome entry in the response |

## Query for Merged Record

This test ensures that the client registry returns the new record (with identifier FHR-080) when the old record (FHR-081) is queried. This resolution ensures that the merge occurred successfully and any attempts to reference an old record results in the new being returned.&#x20;

{% hint style="info" %}
This test uses the business identifiers to ensure the cross referencing is updated, and is the recommended manner for handling record merges. Alternates (such as returning the old record with active of false would place a burden on the client to intelligently handle merges by following, potentially, dozens of "replaced-by" links)
{% endhint %}

```http
GET http://localhost:8080/fhir/Patient?identifier=http%3A%2F%2Fohie.org%2Ftest%2Ftest%7CFHR-081 HTTP/1.1
Accept-Encoding: gzip,deflate
Authorization: BEARER XXXXXXXX
Accept: application/fhir+json
Host: localhost:8080
Connection: Keep-Alive
User-Agent: Apache-HttpClient/4.5.5 (Java/12.0.1)

```

### Expected Behavior

| Requirement | Option | Description                                                                                                                                                                                      |
| ----------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| MUST        |        | <p>Return a bundle with an entry carrying a <code>Patient</code> resource with</p><p>the FHR-080 identifier (i.e. the resource returned should be the survivor</p><p>of the merge operation)</p> |
| MUST        |        | Return HTTP code of 200 OK                                                                                                                                                                       |
| MAY         |        | Return an additional `Patient` entry resource with `active` set to `false` and carrying the now inactive resource.                                                                               |
| SHOULD      |        | Carry a link with type `replaces` indicating that the record returned replaced a previous record.                                                                                                |

## Fetch Merged Record

This test ensures compliance with the IHE PMIR profile by explicitly querying for a resource by logical identifier (rather than business identifier). IHE PMIR provides several options for handling a `READ` or `SEARCH` operation for merged records. All of these options are expressed as alternates in the expected behaviors table.&#x20;

{% hint style="info" %}
This test requires that the logical resource identifier assigned by the iCDR / MPI instance is known by the SUT.
{% endhint %}

```http
GET http://localhost:8080/fhir/Patient/bd9ab237-ee43-4f69-b363-5e016deb690d HTTP/1.1
Accept-Encoding: gzip,deflate
Authorization: BEARER XXXXXXX
Accept: application/fhir+json
Host: localhost:8080
Connection: Keep-Alive
User-Agent: Apache-HttpClient/4.5.5 (Java/12.0.1)
```

### Expected Behavior

| Requirement | Option    | Description                                                                              |
| ----------- | --------- | ---------------------------------------------------------------------------------------- |
| MUST        |           | Return an HTTP 200 OK with the replaced/merged record carrying `active` value of `false` |
| MUST        | ALTERNATE | Return HTTP code of 404 NOT FOUND                                                        |

## Search Merged Record

This test ensures compliance with the IHE PMIR profile by explicitly searching for a resource by logical identifier (rather than business identifier). IHE PMIR provides several options for handling a `SEARCH` operation for merged records. All of these options are expressed as alternates in the expected behaviors table.&#x20;

{% hint style="info" %}
This test requires that the logical resource identifier assigned by the iCDR / MPI instance is known by the SUT.
{% endhint %}

```http
GET http://sut:8080/fhir/Patient?_id=5d0e583f-1fda-4a25-8fbe-f4fb3e876f3c HTTP/1.1
Auhthorization: Bearer XXXXXX
Accept: application/fhir+json
```

### Expected Behavior

| Requirement | Option    | Description                                                                                                                                                                                                                                                       |
| ----------- | --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| MUST        |           | Return an HTTP 200 OK and a `Bundle` with the 0 results.                                                                                                                                                                                                          |
| MUST        | ALTERNATE | <p>Return an HTTP 200 OK and a <code>Bundle</code> with the merged record</p><p>with <code>active</code> set to <code>false</code></p>                                                                                                                            |
| MUST        | ALTERNATE | <p>Return an HTTP 200 OK and a <code>Bundle</code> with 2 results. One </p><p>representing the survivor record (with <code>active</code> of <code>true</code>) and one </p><p>representing the merged record (with <code>active</code> of <code>false</code>)</p> |

## Execute PIXm Query To Validate Merged Record

This test ensures that the updates applied via the PMIR merge are reflected in the PIXm cross-referencing query request. The test harness issues a cross-referencing request to obtain the national health identifier for FHRA-081 (a patient, when registered, did not have a NID however by virtue FHRA-081 was merged into FHR-080 which carries a NID, FHRA-081 should carry a NID).

```http
GET http://localhost:8080/fhir/Patient/$ihe-pix?sourceIdentifier=http%3A%2F%2Fohie.org%2Ftest%2Ftest%7CFHR-081&targetSystem=http%3A%2F%2Fohie.org%2Ftest%2Fnid HTTP/1.1
Accept-Encoding: gzip,deflate
Authorization: BEARER XXXXXXX
Accept: application/fhir+json
Host: localhost:8080
Connection: Keep-Alive
User-Agent: Apache-HttpClient/4.5.5 (Java/12.0.1)

```

### Expected Behavior

| Requirement | Option | Description                                                                                                                   |
| ----------- | ------ | ----------------------------------------------------------------------------------------------------------------------------- |
| MUST        |        | Return an HTTP 200 OK and a `Parameters` as the payload.                                                                      |
| MUST        |        | Return one `targetIdentifier` parameter carrying the NID of NID080                                                            |
| MUST        |        | <p>Return one <code>targetId</code> parameter with a pointer to the surviving record (i.e. <br>not to the merged record) </p> |
