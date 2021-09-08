# HTTP Request Verbs

The HDSI, AMI and BIS all use a common HTTP grammar to operate their REST interfaces.

## Write / Update Operations

### Create New Resource \(POST\)

The HTTP post operation is executed against a root resource type and contains a payload in either XML or JSON \(sync JSON or view model\). The POST operation inserts a new resource \(or collection of resources if creating a Bundle\). If the resource already exists, an HTTP 409 is returned indicating the conflict.

```http
POST /hdsi/Patient HTTP/1.1
Content-Type: application/xml

<Patient xmlns="http://santedb.org/model">
    ...
```

### Create or Update Resource \(POST\)

The HTTP post operation can also be executed against a single instance of a resource. When this method is used, the API will create a new instance OR will update an existing instance of the object.

```http
POST /hdsi/Patient/54558ca5-c093-11ea-9f6f-00155d640b09 HTTP/1.1
Content-Type: application/xml

<Patient xmlns="http://santedb.org/model">
    ...
```

### Update Existing Resource \(PUT\)

The HTTP PUT operation is used to update an existing record on the HDSI, AMI or BIS. If the specified resource does not exist, an HTTP 404 is returned. 

```http
PUT /hdsi/Patient/54558ca5-c093-11ea-9f6f-00155d640b09 HTTP/1.1
Content-Type: application/xml

<Patient xmlns="http://santedb.org/model">
    ...
```

#### Conditional Updates

You can additionally use the conditional update header If-Match or If-None-Match which can be used to update the resource only when the ETAG of the resource matches the ETAG from the client. The reason for doing a conditional update is to prevent concurrent update of the same resource.

Conditional updates will return an HTTP 409 \(Conflict\) whenever the conditional match is not satisfied.

```http
PUT /hdsi/Patient/54558ca5-c093-11ea-9f6f-00155d640b09 HTTP/1.1
Content-Type: application/xml
If-Match: e403940394382743823

<Patient xmlns="http://santedb.org/model">
    ...
```

### Partial Update of Resource \(PATCH\)

The default behavior of the HDSI PUT operation is to replace an object, in its entirety with the value sent to it. For example, if a patient exists in the HDSI, and a client sends an PUT on the patient resource, the HDSI will perform the necessary actions required to ensure that the HDSI patient in its data store matches the patient resource sent.

This means that the PUT operation is really a replacement \(similar to uploading a new copy of a file\). This behavior requires clients to send a complete copy of the resource with modifications to the HDS which can be troublesome when the client only wishes to update part of a resource. In order to overcome this, SanteDB’s HDSI implements the HTTP PATCH method specified in IETF RFC5789. This method allows a client to send a delta of changes to be made to a particular object. The PATCH format is illustrated in , and closely follows the IETF RFC6902 specification

```http
PATCH /hdsi/Patient/54558ca5-c093-11ea-9f6f-00155d640b09 HTTP/1.1
Content-Type: application/xml
If-Match: e403940394382743823

<Patch xmlns="http://santedb.org/model"
```

More documentation of the PATCH operation is documented in the [Constructing Patches article. ](patching.md)

### Obsolete Resource \(DELETE\)

SanteDB provides version tracking of resources in its database and never truly "deletes" objects, rather the object may be placed into one of the inactive states which indicates the resource is no longer active. The inactive states include:

* Obsoleted =&gt; The resource DID exist, however the resource is NO LONGER valid
* Nullified =&gt; The resource NEVER existed, it was entered in error and should be ignored
* Cancelled =&gt; The resource DID exist, however the operation was cancelled

The mode of DELETE verb is to obsolete the object, however you can override this with the X-Delete-Mode header containing either: obsolete, nullify, or cancel to indicate the method of deletion.

```http
DELETE /hdsi/Patient/54558ca5-c093-11ea-9f6f-00155d640b09 HTTP/1.1
Content-Type: application/xml
If-Match: e403940394382743823
X-Delete-Mode: nullify
```

## Read / Query Operations

### Query Resource Type \(GET\)

You may execute a general query against any of the provided resources on the HDSI, AMI or BIS using the query resource type operation. Query resource type is executed via an HTTP GET against the root resource path.

The query parameters are structured using [HDSI Query Syntax](hdsi-query-syntax.md).

```http
GET /hdsi/Patient?name.component.value=PETER HTTP/1.1
Accept: application/xml
Accept-Encoding: gzip
```

The result of a query is a Bundle which contains the offset, count, entry keys and any associated items in the response.

```http
HTTP/1.1 200 OK
Content-Type: application/xml

<Bundle xmlns="http://santedb.org/model">
    <totalResults>100</totalResults>
    <count>20</count>
    <offset>0</offset>
    <item xsi:type="Patient">
        ...
    </item>
</Bundle>
```

#### Conditional Matching / HTTP Caching

The HDSI supports the HTTP conditional headers If-Modified-Since and If-None-Match. These headers control the amount of data sent back when there are no modifications to any data. The If-None-Match header is either the version key or the key of the last modified object in the case of a bundled query, or the primary result in the case of the GET operation.

If the “If” condition fails, then the HDS server will respond with an HTTP 304 \(not modified\).

The HTTP HEAD operation is used to fetch metadata about a particular resource without fetching the resource itself. When a client sends HTTP head, the HDSI interface will respond with data such as version-identifier and sequence of the last edited resource or the metadata of the resource in question. For example, to get all patients named PETER who have been updated since a particular time:

```http
GET /Patient?name.component.value=PETER HTTP/1.1
Authorization: BASIC ZmlkZGxlcjpmaWRkbGVy
Host: demo.openiz.org:8080
If-Modified-Since: Fri, 15 Jul 2016 10:09:39 GMT

HTTP/1.1 304 Not Modified
Content-Length: 0
Server: Microsoft-HTTPAPI/2.0
X-GeneratedOn: 2016-06-22T19:21:30.6871719-04:00
Last-Modified: 2016-06-22T19:21:30.6871719-04:00
```

### Get Resource Instance \(GET\)

A single resource instance is fetched from the server using a GET operation against the specific resource instance on the API. For example:

```http
GET /Patient/fb00e97a-bdfc-403d-8f62-52f8e6846a16 HTTP/1.1
Authorization: BASIC ZmlkZGxlcjpmaWRkbGVy
Host: demo.openiz.org:8080
```

### Get Resource Headers \(HEAD\)

The HEAD operation in SanteDB executes the specified search / retrieve specified on the request, and returns only the headers for that operation. This operation is typically used where response payloads may consume bandwidth unnecessary. Examples of uses of the HEAD operation in practice in SanteDB are:

* Querying the /ami/applet interface to determine if an applet has been updated
* Querying a resource or subscription to determine the last ETag and whether the ETag matches the last downloaded ETag.
* Querying log files to determine their last date of update

{% hint style="info" %}
Instead of executing separate HEAD and then GET operations, you can use the conditional HTTP headers which will return 304 if not modified \(and will save a roundtrip to the server\).
{% endhint %}

### Get Resource History \(GET\)

### Get Resource Version \(GET\)

## Special Operations

### Lock Resource \(LOCK\)

The HTTP LOCK operation in SanteDB is typically used to obtain an exclusive lock on an object, or to lock an object which supports lockout. When using the LOCK HTTP verb against a security resource, any access to that security resource \(such as user, device, or application\) will be prohibited.

For example, to block concurrent editing of a patient, the user interface can lock the resource:

```http
LOCK /SecurirtyUser/fb00e97a-bdfc-403d-8f62-52f8e6846a16 HTTP/1.1
Host: demo.openiz.org:8080
```

Any attempt to perform a PUT, POST, or DELETE against the patient from an authenticated client which is not the client which obtained the lock will result in an HTTP 409 Conflict response error.

### Unlock Resource \(UNLOCK\)

The HTTP UNLOCK operation in SanteDB is used to release a lock on an object, or to release an authentication lock on a security resource \(such as unlocking a user's account\). 

### Checkout Resource \(CHECKOUT\)

There are use cases where clients may wish to obtain an exclusive EDIT lock on a particular resource. This is done by performing an HTTP CHECKOUT on a supported resource \(like Patient, Concept, etc.\). This prevents concurrent editing of the same resource.

```http
CHECKOUT /SecurirtyUser/fb00e97a-bdfc-403d-8f62-52f8e6846a16 HTTP/1.1
Host: demo.openiz.org:8080
Authorization: bearer XXXXXXX
```

The response, if successful, is an `HTTP 204 NO CONTENT` . Any attempt to update the resource other than the principal represented with XXXX will result in a 403.

### Check-in Resource \(CHECKIN\)

The `CHECKIN` verb performs the opposite action as the `CHECKOUT` verb, in that it releases the lock \(if any\) on the specified resource.

### Get Service Parameters \(OPTIONS\)

### Ping Service Availability \(PING\)

The PING operation is a non-standard HTTP verb which is used by the application layer \(on the dCDR\) to determine if the central iCDR server is available. The dCDR also uses the returned Date header to calculate the drift between its own clock and the server.

The response to a PING is an HTTP 204 \(No Content\) response with general service headers such as the server version, the server time, etc.

{% hint style="info" %}
The Date header in the response of the `PING` is used by clients to calculate the time drift between the local device and the server. This is done since NTP services are not always available in all environments.
{% endhint %}

## Associated Resources

## Operations

Operations on the HDSI and AMI represent RPC calls to the server to "do something" rather than a resource manipulation action. Operations start with a `$` sign and may be affixed on an instance or resource level.

Operations always rely on `POST` verbs and always accept an `ApiOperationParameterCollection` object. For example:

```http
POST http://foo.com/hdsi/Patient/$subtractNumbers HTTP/1.1
Content-Type: application/xml

<ApiOperationParameterCollection xmlns="http://santedb.org/operation"
    xmlns:xs="http://www.w3.org/2001/XMLSchema"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <parameter>
        <name>subtrahend</name>
        <value xsi:type="xs:int">30</value>
    </parameter>
    <parameter>
        <name>minuend</name>
        <value xsi:type="xs:int">10</value>
    </parameter>
</ApiOperationParameterCollection>
```



