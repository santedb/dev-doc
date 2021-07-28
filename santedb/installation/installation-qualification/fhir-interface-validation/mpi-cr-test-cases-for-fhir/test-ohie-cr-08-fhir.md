---
description: Patient Merges
---

# TEST: OHIE-CR-08-FHIR

This test ensures that the client registry properly handles merge requests sent by patient identity sources using the PMIR merge mechanism described in IHE Patient Mater Identity Registry. 

## References

* [Integrating the Health Enterprise Patient Master Identity Registry](https://www.ihe.net/uploadedFiles/Documents/ITI/IHE_ITI_Suppl_PMIR.pdf)
* [HL7 FHIR RelatedPerson Resource](http://hl7.org/fhir/relatedperson.html)
* [HL7 FHIR Patient Resource](http://hl7.org/fhir/patient.html)

## Discussion

The PMIR profile makes the assumption that the client is controlling the process of merge by instructing the server to link/de-activate a victim. Since merging is an event which triggers several business rules in the Master Data Management layer, the SanteDB PMIR handler detects this condition \(a client attempting to control linking of patients, which is an internal matter\) and mimics the equivalent behaviors of `ADT^A40` from HL7v2. 

Furthermore, the SanteDB implementation of merging behaves as described in `Chapter 3 - Patient Administration` in HL7 Version 2 \(see: `3.6.2.1.2`\). For example, if two patients from `HOSPITAL_A` are registered as illustrated below \(patient 1 with two identifiers and patient 2 with one\):

![](../../../../../.gitbook/assets/image%20%28395%29.png)

Then a merge requests where Patient 1 is replaced by Patient 2 would result in a merge such that:

![](../../../../../.gitbook/assets/image%20%28396%29.png)

Subsequent requests to query for a patient using `GREEN_TRIANGLE` would result in `Patient 2` being resolved. This behavior differs from the prescribed behavior of PMIR whereby the victim \(in this case Patient 2\) is not returned, or continues to be resolved with an inactive flag.

## Pre-Conditions

Prior to running this test ensure that the pre-conditions from [TEST: OHIE-CR-04](test-ohie-cr-04-fhir.md) and [TEST: OHIE-CR-06](test-ohie-cr-06-fhir.md) have been run.

## Authenticate as TEST\_HARNESS\_FHIR\_A

The test harness authenticates against the SanteMPI IdP using a client\_credentials grant for the test-harness-a account.

```http
POST http://sut:8080/auth/oauth2_token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: sut:8080
Content-Length: 112

grant_type=client_credentials&scope=*&client_id=TEST_HARNESS_A&client_secret=TEST_HARNESS
```

## Register New Patient Identity in TEST\_A

The test harness sends an authenticated request to create a new patient with a new identifier in TEST\_A domain. Patient details:

* Identifier `FHRA-080` in `http://ohie.org/test/test_a` 
* Identifier `NID080` in `http://ohie.org/test/nid` 
* Name: MERGY SMITH
* Gender: Male
* DOB: 1986-05-25

```javascript
{
    "resourceType": "Patient",
    "id": "ohie-cr-08-10-fhir",
    "active": true,
    "identifier": [
      {
        "use": "official",
        "type": {
          "coding": [
            {
              "system": "http://terminology.hl7.org/CodeSystem/v2-0203",
              "code": "PI"
            }
          ]
        },
        "system": "http://ohie.org/test/test_a",
        "value": "FHRA-080",
        "assigner": {
          "display": "Test Harness A Patient Identity"
        }
      },
      {
        "use":"usual",
        "system": "http://ohie.org/test/nhid",
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
  }
```

### Expected Behaviour

| Requirement | Option | Description |
| :--- | :--- | :--- |
| MUST | PMIR Only | Return MessageHeader with response.code = ok |
| MUST |  | Return HTTP code of 201 Created |
| SHOULD | PMIR Only | Include an OperationOutcome entry in the response |
| SHOULD |  | Include a Patient entry in response containing created patient |
| SHOULD |  | Include a link to the master identity with code refer  |

## Execute PIXm Query Patient in TEST\_A

The test harness sends an IHE PIXm query for a patient with identifier FHIRA-080 to the receiver.

```http
GET http://sut:8080/fhir/Patient/$ihe-pix?sourceIdentifier=http://ohie.org/test/test_a|FHRA-080 HTTP/1.1
Auhthorization: Bearer XXXXXX
Accept: application/fhir+json
```

### Expected Behaviour

<table>
  <thead>
    <tr>
      <th style="text-align:left">Requirement</th>
      <th style="text-align:left">Option</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">MUST</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Return HTTP code of 200 OK</td>
    </tr>
    <tr>
      <td style="text-align:left">MUST</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Include an Parameters resource in the response</td>
    </tr>
    <tr>
      <td style="text-align:left">MUST</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <p>Have two parameters carrying the identifier in TEST_A and NID</p>
        <p>with parameter name of targetIdentifier and values FHRA-080 and NID080</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">MUST</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <p>Include a parameter with name targetId which has a resource link</p>
        <p>to the created resource from the previous step.</p>
      </td>
    </tr>
  </tbody>
</table>

## Register Second Patient Identity in TEST\_A

The test harness sends an authenticated request to create a new patient with a new identifier in TEST\_A domain. Patient details:

* Identifier `FHRA-081` in `http://ohie.org/test/test_a` 
* Name: MERGY SMYTHE
* Gender: Male
* DOB: 1986-05-25

```javascript
{
    "resourceType": "Patient",
    "id": "ohie-cr-08-20-fhir",
    "active": true,
    "identifier": [
      {
        "use": "official",
        "type": {
          "coding": [
            {
              "system": "http://terminology.hl7.org/CodeSystem/v2-0203",
              "code": "PI"
            }
          ]
        },
        "system": "http://ohie.org/test/test_a",
        "value": "FHRA-081",
        "assigner": {
          "display": "Test Harness A Patient Identity"
        }
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
  }
```

### Expected Behaviour

| Requirement | Option | Description |
| :--- | :--- | :--- |
| MUST | PMIR Only | Return MessageHeader with response.code = ok |
| MUST |  | Return HTTP code of 201 Created |
| SHOULD | PMIR Only | Include an OperationOutcome entry in the response |
| SHOULD |  | Include a Patient entry in response containing created patient |
| SHOULD |  | Include a link to the master identity with code refer  |

## Execute PIXm Query Patient in TEST\_A

The test harness sends an IHE PIXm query for a patient with identifier FHIRA-081 to the receiver.

```http
GET http://sut:8080/fhir/Patient/$ihe-pix?sourceIdentifier=http://ohie.org/test/test_a|FHRA-081 HTTP/1.1
Auhthorization: Bearer XXXXXX
Accept: application/fhir+json
```

### Expected Behaviour

<table>
  <thead>
    <tr>
      <th style="text-align:left">Requirement</th>
      <th style="text-align:left">Option</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">MUST</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Return HTTP code of 200 OK</td>
    </tr>
    <tr>
      <td style="text-align:left">MUST</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Include an Parameters resource in the response</td>
    </tr>
    <tr>
      <td style="text-align:left">MUST</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Have two parameters carrying the identifier in TEST_A with parameter name
        of targetIdentifier and value FHRA-081.</td>
    </tr>
    <tr>
      <td style="text-align:left">MUST</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <p>Include a parameter with name targetId which has a resource link</p>
        <p>to the created resource from the previous step.</p>
      </td>
    </tr>
  </tbody>
</table>

## Merge FHRA-081 into FHRA-080

In this step the test harness sends a PIMR request to instruct the Client Registry that `FHRA-081` has been replaced by `FHRA-080`.

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
                  "type": {
                    "coding": [
                      {
                        "system": "http://terminology.hl7.org/CodeSystem/v2-0203",
                        "code": "PI"
                      }
                    ]
                  },
                  "system": "http://ohie.org/test/test_a",
                  "value": "FHRA-081",
                  "assigner": {
                    "display": "Test Harness A Patient Identity"
                  }
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
              "link": [
                {
                  "other": {
                    "type": "Patient",
                    "identifier": {
                      "value": "FHRA-080",
                      "system": "http://ohie.org/test/test_a"
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
You will notice that the `link` element in the above message uses the business identifier reference rather than an absolute reference by URL. This is considered best practice when merging on SanteDB server as it abstracts the logical identifier \(which changes as the resource moves between servers\). See: [http://hl7.org/fhir/resource.html\#identifiers](http://hl7.org/fhir/resource.html#identifiers)
{% endhint %}

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

| Requirement | Option | Description |
| :--- | :--- | :--- |
| MUST |  | Return MessageHeader with response.code = ok |
| MUST |  | Return HTTP code of 200 OK |
| SHOULD |  | Include an OperationOutcome entry in the response |

## Query for Merged Record

This test ensures that the client registry returns the new record \(with identifier FHRA-080\) when the old record \(FHRA-081\) is queried. This resolution ensures that the merge occurred successfully and any attempts to reference an old record results in the new being returned. 

{% hint style="info" %}
This test uses the business identifiers to ensure the cross referencing is updated, and is the recommended manner for handling record merges. Alternates \(such as returning the old record with active of false would place a burden on the client to intelligently handle merges by following, potentially, dozens of "replaced-by" links\)
{% endhint %}

```http
GET http://sut:8080/fhir/Patient?identifier=http://ohie.org/test/test_a|FHRA-081 HTTP/1.1
Auhthorization: Bearer XXXXXX
Accept: application/fhir+json
```

### Expected Behavior

<table>
  <thead>
    <tr>
      <th style="text-align:left">Requirement</th>
      <th style="text-align:left">Option</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">MUST</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <p>Return a bundle with an entry carrying a <code>Patient</code> resource with</p>
        <p>the FHRA-080 identifier (i.e. the resource returned should be the survivor</p>
        <p>of the merge operation)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">MUST</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Return HTTP code of 200 OK</td>
    </tr>
    <tr>
      <td style="text-align:left">MAY</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Return an additional <code>Patient</code> entry resource with <code>active</code> set
        to <code>false</code> and carrying the now inactive resource.</td>
    </tr>
  </tbody>
</table>

## Fetch Merged Record

This test ensures compliance with the IHE PMIR profile by explicitly querying for a resource by logical identifier \(rather than business identifier\). IHE PMIR provides several options for handling a `READ` or `SEARCH` operation for merged records. All of these options are expressed as alternates in the expected behaviors table. 

{% hint style="info" %}
This test requires that the logical resource identifier assigned by the iCDR / MPI instance is known by the SUT.
{% endhint %}

```http
GET http://sut:8080/fhir/Patient/5d0e583f-1fda-4a25-8fbe-f4fb3e876f3c HTTP/1.1
Auhthorization: Bearer XXXXXX
Accept: application/fhir+json
```

### Expected Behavior

| Requirement | Option | Description |
| :--- | :--- | :--- |
| MUST |  | Return an HTTP 200 OK with the replaced/merged record carrying `active` value of `false` |
| MUST | ALTERNATE | Return HTTP code of 404 NOT FOUND |

## Search Merged Record

This test ensures compliance with the IHE PMIR profile by explicitly searching for a resource by logical identifier \(rather than business identifier\). IHE PMIR provides several options for handling a `SEARCH` operation for merged records. All of these options are expressed as alternates in the expected behaviors table. 

{% hint style="info" %}
This test requires that the logical resource identifier assigned by the iCDR / MPI instance is known by the SUT.
{% endhint %}

```http
GET http://sut:8080/fhir/Patient?_id=5d0e583f-1fda-4a25-8fbe-f4fb3e876f3c HTTP/1.1
Auhthorization: Bearer XXXXXX
Accept: application/fhir+json
```

### Expected Behavior

<table>
  <thead>
    <tr>
      <th style="text-align:left">Requirement</th>
      <th style="text-align:left">Option</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">MUST</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Return an HTTP 200 OK and a <code>Bundle</code> with the 0 results.</td>
    </tr>
    <tr>
      <td style="text-align:left">MUST</td>
      <td style="text-align:left">ALTERNATE</td>
      <td style="text-align:left">
        <p>Return an HTTP 200 OK and a <code>Bundle</code> with the merged record</p>
        <p>with <code>active</code> set to <code>false</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">MUST</td>
      <td style="text-align:left">ALTERNATE</td>
      <td style="text-align:left">
        <p>Return an HTTP 200 OK and a <code>Bundle</code> with 2 results. One</p>
        <p>representing the survivor record (with <code>active</code> of <code>true</code>)
          and one</p>
        <p>representing the merged record (with <code>active</code> of <code>false</code>)</p>
      </td>
    </tr>
  </tbody>
</table>

## PIXm Query for Merged Record

This test ensures that the updates applied via the PMIR merge are reflected in the PIXm cross referencing query request. The test harness issues a cross referencing request to obtain the national health identifier for FHRA-081 \(a patient, when registered, did not have an NID however by virtue FHRA-081 was merged into FHR-080 which carries a NID, FHRA-081 should carry a NID\).

```http
GET http://sut:8080/fhir/Patient/$ihe-pix?sourceIdentifier=http://ohie.org/test/test_a&targetDomain=http://ohie.org/test/nid HTTP/1.1
Auhthorization: Bearer XXXXXX
Accept: application/fhir+json
```

### Expected Behavior

| Requirement | Option | Description |
| :--- | :--- | :--- |
| MUST |  | Return an HTTP 200 OK and a `Parameters` as the payload. |
| MUST |  | Return one `targetIdentifier` parameter carrying the NID of NID080 |
| MUST |  | Return one `targetId` parameter with a pointer to the surviving record \(i.e.  not to the merged record\)  |

