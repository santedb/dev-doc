# MDM Extensions for HDSI

The [Master Data Management](../../../architecture/data-storage-patterns/master-data-storage.md) plugin for SanteDB provides controls for the management of the MDM metadata via the HDSI interface using custom interfaces.

{% hint style="warning" %}
When using the MDM extensions on the dCDR \(like in the user interface, or on a client\) you must provide the `_upstream=true` indicator so the dCDR service sends the original request to the central server directly. This means that these functions should only be called when online and connected to the iCDR
{% endhint %}

{% hint style="success" %}
It is entirely possible to perform the same operations manually by manipulating the `EntityRelationship` resources in the CDR. However this method is discouraged as `EntityRelationship`properties require specific attributes/values in order for MDM to function correctly.
{% endhint %}

## Operations

The operations provided by the MDM extension plugins actually kickoff jobs and operations on the SanteDB server. These are equivalent to calling the Job management interface on the AMI.

### Clear

The clear operation clears the entire database of all MDM linkages. Depending on the parameters use, this function will completely remove all MDM links. 

{% hint style="warning" %}
It is only recommended that this operation be performed if you are disabling MDM \(i.e. plan on turning off the MDM layer\) or if you are experimenting and want to clear the automatically generated links.
{% endhint %}

```http
POST /hdsi/Patient/$mdm-clear HTTP/1.1
Content-Type: application/json

{
    "$type":"ApiOperationParameterCollection",
    "parameter": [
        {
            "name":"includeVerified",
            "value": false
        },
        {
            "name":"globalReset",
            "value": false
        },
        {
            "name":"linksOnly",
            "value": false
        } 
    ]
}
```

| Parameter | Value |
| :--- | :--- |
| includeVerified | If true the clear operation will remove all MDM links \(ignore, candidates, etc.\)  including those which have been adjudicated by a human and verified. When  false only automatic links are moved. |
| globalReset | If true the clear operation will perform a global reset on all MDM links in the system. This includes resetting MDM master, candidate, ignore, and record of truth links. |
| linksOnly | When true, only links are removed and any targets of those links \(like master records, etc.\) are left orphaned. It is recommended to leave this value as FALSE |

### Rematch

The re-match operation instructs the iCDR to start the process of re-matching a patient object based on the data in the current database. 

#### Global Rematch

The global rematch operation will kickoff the master MDM re-matching job. 

```http
POST /hdsi/Patient/$mdm-rematch HTTP/1.1
Content-Type: application/json

{
    "$type":"ApiOperationParameterCollection",
    "parameter": [
        {
            "name":"clear",
            "value": false
        }
    ]
}
```

This operation kicks off the associated Patient MDM match job.

#### Instance Rematch

The instance rematch operation instructs the iCDR to perform a re-matching operation on a specific instance of a resource.

```http
POST /hdsi/Patient/2fcaf2ec-e6b2-4786-bfbe-e5848dffe268/$mdm-rematch HTTP/1.1
Content-Type: application/json

{
    "$type":"ApiOperationParameterCollection",
    "parameter": [
        {
            "name":"clear",
            "value": false
        }
    ]
}
```

## Resources

The linkages in the MDM layer can be controlled and queried via the extended resources on the API. These resources control the links between a master record and the locals \(or candidate locals\). 

When a property is scoped to a particular instance of a resource, the resource UUID can represent a `LOCAL` record \(in which case results are the corresponding `MASTER` records\) or the UUID can represent a `MASTER` record \(in which case the results are the corresponding `LOCAL` records\). Operations on global resources are match pairs since there is no context.

### MDM Candidates \(mdm-candidate\)

An MDM match candidate exists between two records when the matching engine determines either:

* There is exactly one other record in the solution classified as `Match` and `autoLink` is turned off, or
* There are more than one other records in the solution classified as `Match` regardless of `autoLink`, or
* There are more than one other records in the solution classified as `Probable`

#### Get Global MDM Candidates

Gets a list of global MDM candidates which have been established / detected on the iCDR server.

```http
GET /hdsi/Patient/mdm-candidate HTTP/1.1
Accept: application/json
```

The result of this operation is a list of `EntityRelationship` pairs which represent the candidate local `holder` and the candidate master `target`.

```http
HTTP/1.1 200 OK
Content-Length: XXXX
Content-Type: application/json

{
    "$type": "Bundle",
    "resource": [
        {
            "$type" : "EntityRelationship",
            "holder": "5ac04a36-b521-4bc1-8255-6463c0083ae8",
            "target" : "f8f92db2-e48e-4b6c-951d-b42e06c5c4d4",
            "relationshipType" : "56cfb115-8207-4f89-b52e-d20dbad8f8cc",
            "score" : 0.666666667
        }
    ]
}
```

{% hint style="info" %}
You can use an accept header of application/json+viewModel to fetch the holder and target entities without a re-fetch.
{% endhint %}

#### Get Candidates for Instances

Gets a list of all MDM candidate instances for a particular resource instance. Since this method has a resource instance scope, it does not return the relationship objects, rather it returns the actual instances of the candidates \(either `MASTER` records to which the current local is a candidate or `LOCAL` records for which current master has candidates\).

```http
GET /hdsi/Patient/5ac04a36-b521-4bc1-8255-6463c0083ae8/mdm-candidate HTTP/1.1
Accept: application/json
```

The results of this operation is a bundle with the candidate patient instances.

```http
HTTP/1.1 200 OK
Content-Length: XXXX
Content-Type: application/json

{
    "$type": "Bundle",
    "resource": [
        {
            "$type" : "Patient",
            "id" : "f8f92db2-e48e-4b6c-951d-b42e06c5c4d4",
            ...
            "tag" : [
                {
                    "name":"$generated",
                    "value":"true"
                },
                {
                    "name":"$match.score",
                    "value":"0.66667"
                }
            ]
        }
    ]
}
```

The `$match.score` tag on the returned object is the original score that candidate had with the focal record.

#### Remove Candidate from Instance

The remove candidate resource operation is a `DELETE` against the candidate record and instructs the matcher to never consider the record as a candidate again \(establishes an IGNORE record\). 

```http
DELETE /hdsi/Patient/5ac04a36-b521-4bc1-8255-6463c0083ae8/mdm-candidate/f8f92db2-e48e-4b6c-951d-b42e06c5c4d4 HTTP/1.1
Accept: application/json
```

#### Get Match Report for Instance

This operation instructs the MDM handler to retrieve a detailed match report between the instance and the candidate record.

```http
GET /hdsi/Patient/5ac04a36-b521-4bc1-8255-6463c0083ae8/mdm-candidate/f8f92db2-e48e-4b6c-951d-b42e06c5c4d4 HTTP/1.1
Accept: application/json
```

The results of this operation a match report object which details the results of the matching:

```http
HTTP/1.1 200 OK
Content-Length: XXXX
Content-Type: application/json

{
    "$type": "MatchReport",
    "input": "5ac04a36-b521-4bc1-8255-6463c0083ae8",
    "results" : [
        {
            "score" : 2.167777,
            "strength": 0.66667,
            "record": "f8f92db2-e48e-4b6c-951d-b42e06c5c4d4",
            "classification": "Match",
            "vectors": [
                {
                    "name": "dateOfBirth",
                    "evaluated": true,
                    "m": 0.75,
                    "u": 0.25,
                    "score": 1.587,
                    "a": "1983-05-01",
                    "b": "1983-05-01"
                }
            ]
        }
    ]
}
```

### MDM Ignored \(mdm-ignore\)

An ingnore link is used to signal that a user has reviewed a duplicate and determined that the indicated link is definitely not a candidate/duplicate.

#### Get Ignored Candidates for Instance

This resource fetches all candidates for an instance which were confirmed to be "not a match" \(i.e. are ignored\).

```http
GET /hdsi/Patient/5ac04a36-b521-4bc1-8255-6463c0083ae8/mdm-ignore HTTP/1.1
Accept: application/json
```

The result of this is a list of ignored records which the matcher will never consider for matching.

```http
HTTP/1.1 200 OK
Content-Length: XXXX
Content-Type: application/json

{
    "$type": "Bundle",
    "resource": [
        {
            "$type" : "Patient",
            "id" : "f8f92db2-e48e-4b6c-951d-b42e06c5c4d4",
            ...
            "tag" : [
                {
                    "name":"$generated",
                    "value":"true"
                }
            ]
        }
    ]
}
```

#### Un-Ignore Candidate from Instance

This resource action instructs the MDM layer to un-ignore a previously ignored link between a candidate and its master. When a candidate is "un-ignored" any subsequent execution of the matching logic may re-identify the ignored link as a potential candidate match.

```http
DELETE /hdsi/Patient/5ac04a36-b521-4bc1-8255-6463c0083ae8/mdm-ignore/f8f92db2-e48e-4b6c-951d-b42e06c5c4d4 HTTP/1.1
Accept: application/json
```

### MDM Established Links \(mdm-link\)

#### Get Established MDM Link for Instance

This resource represents the established links between a master and local records. The resource is essentially equivalent to calling a query to `EntityRelationship?relationshipType.mnemonic=MDM-Master` with the exception that the caller does not need to know whether the identifier passed as the parameter is a master or a local record.

```http
GET /hdsi/Patient/5ac04a36-b521-4bc1-8255-6463c0083ae8/mdm-link HTTP/1.1
Accept: application/json
```

The result of this call is a bundle with the contained local resources.

```http
HTTP/1.1 200 OK
Content-Length: XXXX
Content-Type: application/json

{
    "$type": "Bundle",
    "resource": [
        {
            "$type" : "Patient",
            "id" : "f8f92db2-e48e-4b6c-951d-b42e06c5c4d4",
            ...
            "tag" : [
                {
                    "name":"$generated",
                    "value":"true"
                }
            ]
        }
    ]
}
```

#### Detach Established MDM Link for Instance

The detach MDM link action is performed by `DELETE` the `mdm-link` between two objects. This call does not rely on the order of parameters so long as the scoping key and the child key represent a MASTER/LOCAL pair. For example, this call:

```http
DELETE /hdsi/Patient/5ac04a36-b521-4bc1-8255-6463c0083ae8/mdm-link/f8f92db2-e48e-4b6c-951d-b42e06c5c4d4 HTTP/1.1
Accept: application/json
```

Is the same as this call:

```http
DELETE /hdsi/Patient/f8f92db2-e48e-4b6c-951d-b42e06c5c4d4/mdm-link/5ac04a36-b521-4bc1-8255-6463c0083ae8 HTTP/1.1
Accept: application/json
```

#### Attach MDM Link for Instance

The attach MDM link operation on the `mdm-link` resource ensures that only a LOCAL record is linked with a MASTER record. This differs from a MERGE operation where LOCAL&gt;LOCAL and MASTER&gt;MASTER merges can be performed \(and it called via the `$merge` operation since `$merge` does not rely on MDM logic\). 

{% hint style="info" %}
You can still perform an MDM attachment using the `$merge` operation, however the source and target UUIDs must be a local and master respectively.
{% endhint %}

To link an instance the caller must `POST` an `Reference`  with the `id` carrying the UUID of the master to which the attaching is to occur \(or if the focus UUID on the URL is a MASTER then the UUID of the local\).

```http
POST /hdsi/Patient/5ac04a36-b521-4bc1-8255-6463c0083ae8/mdm-link HTTP/1.1
Content-Type: application/json

{
    "$type": "Reference",
    "id": "f8f92db2-e48e-4b6c-951d-b42e06c5c4d4"
}
```

All properties other than `id` in the `Entity` are ignored.

