# API Responses

The HDSI, AMI and BIS all behave in a similar manner at the HTTP layer. Responses from the server use the HTTP error response code to indicate the classification of error, and an error result in JSON is returned to the caller so that specific details of the error can be parsed and conveyed to end-users.

### HTTP Response Codes

| **Code** | **Error** | **Description** |
| :--- | :--- | :--- |
| 200 | OK / No Error | This error condition indicates that the entire operation succeeded and the response represents the desired operation. |
| 201 | Created | This status code indicates that the resource was created on the server and additional processing may occur. |
| 204 | No Content | The action succeeded, however there is no content to the response. |
| 302 | Moved | This status code indicates a redirect. This is used when a request is made to an HDSI interface on a server where a remote IDataPersistence is configured \(such as in a load balancing or migration scenario\). |
| 400 | Bad Request | This response code indicates that there was no possible way for the HDSI to comprehend the request sent to it. This is typically done when a low level processing instruction fails \(such as bad compression data\) |
| 401 | Unauthorized | This response code indicates that the requested resource requires permissions which are above the current permission set of the user. This may indicate that the current user is ANONYMOUS and is trying to access a protected resource, OR may indicate a desire by the HDSI interface for the client to elevate themselves. |
| 403 | Forbidden | This response code indicates that the authorized user is not permitted to access the requested resource. This represents a full DENY policy decision. |
| 404 | Not Found | This response code indicates that the resource requested cannot be found. |
| 405 | Method not allowed | This response code indicates that the client attempted to perform an operation on the HDSI interface which is not permitted. |
| 409 | Conflict | This response code indicates that an update failed because of a formal validation constraint. Or a patch application failed due to test failure. |
| 410 | Gone | This response code indicates that the resource being requested DID exist, however has since been obsoleted. |
| 415 | Unsupported Media Type | This response code indicates that it is not possible for the HDSI to process the request content. This error typically occurs when the client is submitting data which is not JSON nor XML. |
| 422 | Entity could not be processed | The server understood the request \(content/type and content\) however was unable to process the request due to some state issue or business rule violation. |
| 500 | Server Error | This error indicates that the server encountered an error while trying to perform the operation. |
| 503 | Service Unavailable | This error indicates that the HDSI service is temporarily unavailable due to current startup or partial startup \(i.e. an error occurred starting the HDS\). |

### Error Response Payload

Whenever an error condition is encountered, the API will return a structured JSON or XML error response / payload. This payload indicates the reason for the failure. The payload in XML is illustrated below:

```http
HTTP/1.1 500 Internal Server Error
Date: Thu, 27 Aug 2020 20:39:09 GMT
Content-Type: application/xml
Content-Length: 1716
Connection: keep-alive
X-PoweredBy: SanteDB 2.0.26.36666 (Kelowna)
X-GeneratedOn: 2020-08-27T16:39:09.4334858-04:00

<?xml version="1.0"?>
<RestServiceFault xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://santedb.org/fault">
  <type>TypeOfException</type>
  <message>Human Readable Message</message>
  <stack>
         In Debug Mode
         The Stack Trace
         Where The Error Was Thrown
  </stack>
  <policyOutcome>Outcome of Policy Decision</policyOutcome>
  <policy>ID of Policy</policy>
  <rule id="id-of-business-rule-violated" priority="W" type="UUID">Description of business rule violation</rule>
  <cause>
         ... Another Service Fault ...
  </cause>
</RestServiceFault>
```

