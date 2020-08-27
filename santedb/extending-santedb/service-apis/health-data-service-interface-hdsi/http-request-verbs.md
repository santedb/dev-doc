# HTTP Request Verbs

The HDSI, AMI and BIS all use a common HTTP grammar to operate their REST interfaces.

## Write / Update Operations

### Create New Resource \(POST\)

The HTTP post operation is executed against a root resource type and contains a payload in either XML or JSON \(sync JSON or view model\). The POST operation inserts a new resource \(or collection of resources if creating a Bundle\). If the resource already exists, an HTTP 409 is returned indicating the conflict.

```text
POST /hdsi/Patient HTTP/1.1
Content-Type: application/xml

<Patient xmlns="http://santedb.org/model">
    ...
```

### Create or Update Resource \(POST\)

The HTTP post operation can also be executed against a single instance of a resource. When this method is used, the API will create a new instance OR will update an existing instance of the object.

```text
POST /hdsi/Patient/54558ca5-c093-11ea-9f6f-00155d640b09
Content-Type: application/xml

<Patient xmlns="http://santedb.org/model">
    ...
```

### Update Existing Resource \(PUT\)

The HTTP PUT operation is used to update an existing record on the HDSI, AMI or BIS. If the specified resource does not exist, an HTTP 404 is returned. 

```text
PUT /hdsi/Patient/54558ca5-c093-11ea-9f6f-00155d640b09
Content-Type: application/xml

<Patient xmlns="http://santedb.org/model">
    ...
```

#### Conditional Updates

You can additionally use the conditional update header If-Match or If-None-Match which can be used to update the resource only when the ETAG of the resource matches the ETAG from the client. The reason for doing a conditional update is to prevent concurrent update of the same resource.

Conditional updates will return an HTTP 409 \(Conflict\) whenever the conditional match is not satisfied.

```text
PUT /hdsi/Patient/54558ca5-c093-11ea-9f6f-00155d640b09
Content-Type: application/xml
If-Match: e403940394382743823

<Patient xmlns="http://santedb.org/model">
    ...
```

### Partial Update of Resource \(PATCH\)

The default behavior of the HDSI PUT operation is to replace an object, in its entirety with the value sent to it. For example, if a patient exists in the HDSI, and a client sends an PUT on the patient resource, the HDSI will perform the necessary actions required to ensure that the HDSI patient in its data store matches the patient resource sent.

This means that the PUT operation is really a replacement \(similar to uploading a new copy of a file\). This behavior requires clients to send a complete copy of the resource with modifications to the HDS which can be troublesome when the client only wishes to update part of a resource. In order to overcome this, SanteDB’s HDSI implements the HTTP PATCH method specified in IETF RFC5789. This method allows a client to send a delta of changes to be made to a particular object. The PATCH format is illustrated in , and closely follows the IETF RFC6902 specification

```text
PATCH /hdsi/Patient/54558ca5-c093-11ea-9f6f-00155d640b09
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

```text
DELETE /hdsi/Patient/54558ca5-c093-11ea-9f6f-00155d640b09
Content-Type: application/xml
If-Match: e403940394382743823
X-Delete-Mode: nullify
```

## Read / Query Operations

### Query Resource Type \(GET\)

You may execute a general query against any of the provided resources on the HDSI, AMI or BIS using the query resource type operation. Query resource type is executed via an HTTP GET against the root resource path.

The query parameters are structured using [HDSI Query Syntax](hdsi-query-syntax.md).

```text
GET /hdsi/Patient?name.component.value=PETER
Accept: application/xml
Accept-Encoding: gzip
```

The result of a query is a Bundle which contains the offset, count, entry keys and any associated items in the response.

```text
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

```text
GET /Patient?name.component.value=PETER
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

```text
GET /Patient/fb00e97a-bdfc-403d-8f62-52f8e6846a16
Authorization: BASIC ZmlkZGxlcjpmaWRkbGVy
Host: demo.openiz.org:8080
```

### Get Resource Headers \(HEAD\)

The HEAD operation 

### Get Resource History \(GET\)

### Get Resource Version \(GET\)



## Special Operations

### Lock Resource \(LOCK\)

### Unlock Resource \(UNLOCK\)

### Get Service Parameters \(OPTIONS\)

### Ping Service Availability \(PING\)

## Associated Resources

## Control Parameters

### Controlling Response Format

The HDSI, AMI and BIS all support a variety of response formats which are controlled by the Accept header. Valid accept headers are:

| Accept | Format |
| :--- | :--- |
| application/xml | XML format optimized for synchronization interfaces |
| application/json | JSON format optimized for synchronization interfaces |
| application/json+sdb-viewmodel | JSON format optimized for HTML rendering |

### Request / Response Compression

SanteDB is designed to work in low-resource environments with high latency narrowband networks. This means that SanteDB provides a variety of data compression algorithms which can be specified when interacting with the server.

Request payloads which are compressed are indicated using the Content-Encoding HTTP header and the Accept-Encoding HTTP header to control the compression of the response.

```text
PUT /hdsi/Patient/fb00e97a-bdfc-403d-8f62-52f8e6846a16
Authorization: BASIC ZmlkZGxlcjpmaWRkbGVy
Host: demo.openiz.org:8080
Content-Encoding: gzip
Accept-Encoding: gzip

<<< GZIP COMPRESSED BINARY PAYLOAD >>>

HTTP/1.1 201 Created
Content-Encoding: gzip
X-CompressResponseStream: gzip

<<< GZIP COMPRESSED BINARY PAYLOAD >>>
```

The compression algorithms supported by SanteDB are:

<table>
  <thead>
    <tr>
      <th style="text-align:left">Algorithm</th>
      <th style="text-align:left">Header</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">GZIP Compress</td>
      <td style="text-align:left">gzip</td>
      <td style="text-align:left">Uses the GZIP compression algorithm for payloads (default)</td>
    </tr>
    <tr>
      <td style="text-align:left">BZIP2 Compress</td>
      <td style="text-align:left">bzip2</td>
      <td style="text-align:left">Uses the BZIP2 compression algorithm</td>
    </tr>
    <tr>
      <td style="text-align:left">Deflate Compress</td>
      <td style="text-align:left">deflate</td>
      <td style="text-align:left">Uses the ZIP deflate compression algorithm (df)</td>
    </tr>
    <tr>
      <td style="text-align:left">LZMA Compress</td>
      <td style="text-align:left">lzma</td>
      <td style="text-align:left">
        <p>Uses the LZMA / 7ZIP compression algorithm.</p>
        <p>This option uses more CPU resources on compression however results in
          much slower payload sizes.</p>
      </td>
    </tr>
  </tbody>
</table>

