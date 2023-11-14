# Health Data Service Interface (HDSI)

## Controlling Response Format

The HDSI, AMI and BIS all support a variety of response formats which are controlled by the `Accept` header. Valid accept headers are:

| Accept                         | Format                                               |
| ------------------------------ | ---------------------------------------------------- |
| application/xml                | XML format optimized for synchronization interfaces  |
| application/json               | JSON format optimized for synchronization interfaces |
| application/json+sdb-viewmodel | JSON format optimized for HTML rendering             |

### XML

XML is the preferred method of transport for the HDSI, AMI and BIS. XML has several advantages over the JSON format messages, especially when running SanteDB in a full .NET Framework Environment. These benefits include:

* Pre-Compiled Serialization - The .NET framework pre-compiles serialization and parsing libraries which make the reading and writing of XML much faster.&#x20;
* Use of Streams - When using XML serialization the parser and serializer classes use .NET memory streams and stream readers. This is much faster and less memory intensive than the string based processing that the JSON formats use.
* Easy Validation / Translation - When using XML you can leverage the XSD and XSLT functions of XML to easily validate and transform messages. SanteDB provides schemas for all payload classes in XSD.

Additionally, SanteDB offers content compression on response and request payloads. When compressed the size of the payloads over the wire are negligible when compared to compressed JSON formats.

### Sync JSON

JSON format payloads which are a 1:1 map of the XML payloads can be obtained using the synchronization JSON format. These payloads are small since they make the assumption that the caller already has prior knowledge of referenced data.&#x20;

When using this format, the response objects are serialized (using JSON.NET) directly to the wire. There is a performance penalty however, since JSON.NET uses string manipulation to achieve parsing and serialization.

### ViewModel JSON

ViewModel JSON is a convenience method of serialization, and is intended for use when the client may not have the ability (or desire) to synchronize data with the entire server. ViewModel JSON works by expanding (lazy loading) properties and including them as nested objects in the response payload.&#x20;

This is extremely helpful when rendering data, consider, for example, the following patient result:

```http
GET http://my.server/hdsi/Patient/0ea6e373-5763-41a6-a5f3-daa0b2c01b62 HTTP/1.1
Accept: application/json
Accept-Encoding: gzip
```

The response of this message would be:

```http
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 3945
Content-Encoding: gzip

{
    "$type" : "Patient",
    ...
    "relationship": [
        {
            "relationshipType": "24380d53-ea22-4820-9f06-8671f774f133",
            "target": "0f4ae60a-c6af-4cf3-a786-a52b4401df65"
        }
    ]
}
```

This API is useful if the caller has an idea what the `relationshipType` UUID means and what the `target` entity is (they can, of course fetch these). However, when using the view model classes:

```http
GET http://my.server/hdsi/Patient/0ea6e373-5763-41a6-a5f3-daa0b2c01b62 HTTP/1.1
Accept: application/json+sdb-viewmodel
Accept-Encoding: gzip
```

The response will comprise of a JSON bundle with additional contextual information.

```http
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 3945
Content-Encoding: gzip

{
    "$type" : "Patient",
    ...
    "relationship": {
        "Brother": [
            {
                "$type": "EntityRelationship",
                "relationshipType": "24380d53-ea22-4820-9f06-8671f774f133",
                "target": "0f4ae60a-c6af-4cf3-a786-a52b4401df65",
                "targetModel": {
                    "$type": "Person",
                    ...
                }
            }
        ]
    }
}
```

While this consumes more bandwidth, it does save roundtrips to the server.

## Request / Response Compression

SanteDB is designed to work in low-resource environments with high latency narrowband networks. This means that SanteDB provides a variety of data compression algorithms which can be specified when interacting with the server.

Request payloads which are compressed are indicated using the Content-Encoding HTTP header and the Accept-Encoding HTTP header to control the compression of the response.

```http
PUT /hdsi/Patient/fb00e97a-bdfc-403d-8f62-52f8e6846a16 HTTP/1.1
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

| Algorithm        | Header  | Description                                                                                                                                                |
| ---------------- | ------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| GZIP Compress    | gzip    | Uses the GZIP compression algorithm for payloads (default)                                                                                                 |
| BZIP2 Compress   | bzip2   | Uses the BZIP2 compression algorithm                                                                                                                       |
| Deflate Compress | deflate | Uses the ZIP deflate compression algorithm (df)                                                                                                            |
| LZMA Compress    | lzma    | <p>Uses the LZMA / 7ZIP compression algorithm. </p><p>This option uses more CPU resources on compression however results in much slower payload sizes.</p> |

## Related Topics

{% content-ref url="http-request-verbs.md" %}
[http-request-verbs.md](http-request-verbs.md)
{% endcontent-ref %}

{% content-ref url="hdsi-query-syntax/" %}
[hdsi-query-syntax](hdsi-query-syntax/)
{% endcontent-ref %}

{% content-ref url="digitally-signed-visual-code-api.md" %}
[digitally-signed-visual-code-api.md](digitally-signed-visual-code-api.md)
{% endcontent-ref %}

{% content-ref url="hdsi-query-syntax/" %}
[hdsi-query-syntax](hdsi-query-syntax/)
{% endcontent-ref %}

{% content-ref url="api-responses.md" %}
[api-responses.md](api-responses.md)
{% endcontent-ref %}

{% content-ref url="patching.md" %}
[patching.md](patching.md)
{% endcontent-ref %}

{% content-ref url="matching-extensions-for-hdsi.md" %}
[matching-extensions-for-hdsi.md](matching-extensions-for-hdsi.md)
{% endcontent-ref %}

