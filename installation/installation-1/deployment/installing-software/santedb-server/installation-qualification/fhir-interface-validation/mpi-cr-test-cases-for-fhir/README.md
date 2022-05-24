# MPI/CR Test Cases for FHIR

## Summary

These tests are intended to allow for validation of the SanteMPI operating as a national scale client registry within an OpenHIE context. Although FHIR is used as an underlying standard, there are particular behaviors/requirements which are not captured in FHIR or even within IHE technical frameworks.

SanteMPI acts as a custodian of patient master identities, as such it is important to ensure that the FHIR interfaces are properly configured and behave. This test suite is based on the following underlying documents/assets:

* OpenHIE Test Framework for HL7v2 Messages
* IHE Technical Frameworks related to patient management:
  *    [Patient Demographics Query for Mobile](https://www.ihe.net/uploadedFiles/Documents/ITI/IHE\_ITI\_Suppl\_PDQm.pdf)
  * [Patient Identity Cross Referencing for Mobile](https://www.ihe.net/uploadedFiles/Documents/ITI/IHE\_ITI\_Suppl\_PIXm.pdf)
  * [Patient Master Identity Registry](https://www.ihe.net/uploadedFiles/Documents/ITI/IHE\_ITI\_Suppl\_PMIR.pdf) &#x20;

All implementations of FHIR interfaces in SanteDB are subject to the [FHIR Implementation Notes ](../../../../../../../../operations-1/standard-operating-procedures/hl7-fhir/#fhir-implementation)provided, including limitations on `fullUrl` , identifiers, and offsite resources.&#x20;

## SOAP-UI Test Cases

All of the test cases expressed on the wiki using FHIR have been expressed in a SOAP-UI project available on the [SanteMPI GitHub](https://github.com/santedb/santempi/blob/master/SanteMPI-Test-Cases-soapui-project.xml) project page. You can use [SmartBear SOAP-UI](https://www.soapui.org/downloads/latest-release/) to execute these tests.&#x20;

By default the test  cases use `http://localhost:8080` as the iCDR binding.

## Patient Registration Test Cases

The test cases which involve the merging/creation/updating of patient can be submitted to SanteMPI in three ways. The create tests only specify the contents of a bundle/patient being tested, and do not include any wrapper (such as MessageHeader) specifications.&#x20;

### POST Patient Resource

For simple registration of patients in SanteMPI, the patient resource may be used and POSTed directly. This is the simplest way to execute the transactions.&#x20;

```http
POST http://sut:8080/fhir/Patient HTTP/1.1
Content-Type: application/fhir+json
Authorization: bearer XXXXXXX

{
    "resourceType" : "Patient"
    ...
```

### POST Transaction Bundle

A transaction bundle can be POST(ed) directly to the FHIR Bundle endpoint with necessary information (such as related persons, organizations, etc.) as a transaction to the /fhir/Bundle endpoint. Such transactions are required to have the bundle type of "transaction" selected.

```http
POST http://sut:8080/fhir/Bundle HTTP/1.1
Content-Type: application/fhir+json
Authorization: bearer XXXXXX

{
    "resourceType": "Bundle",
    "type": "transaction",
    "entry": [
        {
            "fullUrl": "Patient/1",
```

{% hint style="info" %}
Any references in the bundle are resolved first from within the bundle using the local reference and then using existing internal data within the SanteMPI instance. It is recommended that senders of bundles include all necessary information and use local references, or query the SanteMPI instance for SanteMPI's UUID for these resources.
{% endhint %}

### Messaging / PMIR

You can also post a FHIR message bundle to either `/fhir/Bundle` or to `/fhir/$process-message`. When sending a request to `/fhir/$process-message` you must use a FHIR Parameters resource as specified in the [Process Message operation definition](https://www.hl7.org/fhir/R4/messageheader-operation-process-message.html). If using PMIR, you should post a message bundle to the `/fhir/Bundle` endpoint.

```http
POST http://sut:8080/fhir/Bundle HTTP/1.1
Content-Type: application/fhir+json
Authorization: bearer XXXXXXX

{
    "resourceType": "Bundle",
    "type": "message",
    "entry": [
        {
            "fullUrl": "MessageHeader/1",
            "resource": {
                "resourceType": "MessageHeader",
```

The minimal bundle which is required to process a PMIR message has:

* A `MessageHeader` with the appropriate PMIR operation type
* A single entry being a `Bundle`with type history

```javascript
{
    "resourceType": "Bundle",
    "type": "message",
    "entry": [
        {
            "fullUrl": "MessageHeader/1",
            "resource": {
                "resourceType": "MessageHeader",
                "id": "1",
                "eventUri": "urn:ihe:iti:pmir:2019:patient-feed",
                "source": {
                    "endpoint": "http://example.com/patientSource"
                },
                "focus": [
                    {
                        "reference": "Bundle/1"
                    }
                ],
                "destination": [
                    {
                        "endpoint": "http://sut:8080/fhir/Bundle"
                    }
                ]
            }
        },
        {
            "fullUrl": "Bundle/1",
            "resource": {
                "resourceType": "Bundle",
                "type": "history",
                "entry": [
                    {
                        "fullUrl": "Patient/1",
                        "resource": {
                            "resourceType": "Patient",
                         /* Other Patient Details Here */
                            
                        }
                    }
                ]
            }
        }
    ]
}
```

### PMIR Implementation Notes (Master Merge)

SanteMPI maintains strict authority over which systems are permitted to perform `MASTER->MASTER` merges. The SanteMPI implementation of PMIR allows callers (such as an EMR, LAB, HIS, etc.) to merge only their own LOCAL records in a `LOCAL->LOCAL` merge using the `replaces` relationship type.&#x20;

Attempting to merge two master identities together will result in a new LOCAL record being established for the caller's data domain and a LOCAL->LOCAL merge occurring. In order to permit EMRs or other callers to perform MASTER->MASTER merge you should add the `Unrestricted MDM` policy to the application or device credentials for that caller.&#x20;

{% hint style="info" %}
Allowing MASTER->MASTER merging from external callers is not actively tested or maintained by the SanteMPI team, and should be used with caution as it allows any user on that application to have unrestricted control over the master identities in your SanteMPI deployment.
{% endhint %}
