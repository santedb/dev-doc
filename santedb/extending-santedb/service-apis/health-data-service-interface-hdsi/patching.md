# Patching

SanteDB's REST API supports patching of resources. Patching follows [IETF RFC 5789](https://tools.ietf.org/html/rfc5789) pattern and has the following rules:

* The patch must be applied to a specific instance of a resource
* The patch must include the If-Match header with the etag of the last version the client has \(and wishes to patch\)

### Constructing a Patch

The format of a patch in SanteDB is illustrated below:

```markup
<Patch xmlns="http://santedb.org/model">
    <appliesTo type="Patient|Place|Entity...">
        <id>9fdb557d-2e2f-4fe5-a193-e1cf8cf49bc4</id>
    </appliesTo>
    <change op="Test|Replace|Remove|Add" path="pathInObject">
        <value>
            object
        </value>
    </change>
</Patch>
```

For example, if we wanted to replace the Legal name of a patient, the patch would be as follows:

```markup
<Patch xmlns="http://santedb.org/model">
    <appliesTo type="Patient">
        <id>1c8c9aa3-abb8-48ee-992d-8f0c524ce40c</id>
    </appliesTo>
    <!-- Remove existing Legal Name -->
    <change op="Remove" path="name">
        <value>
            <EntityName>
                <use>effe122d-8d30-491d-805d-addcb4466c35</use>
            </EntityName>
        </value>
    </change>
    <change op="Add" path="name">
        <value>
            <EntityName>
                <use>effe122d-8d30-491d-805d-addcb4466c35</use>
                <component>
                    <value>Jim</value>
                </component>
            </EntityName>
    </change>
</Patch>
```

Alternately you can simply identify a specific instance to be removed by substituting the use qualifier with a UUID:

```markup
<change op="Remove" path="name">
    <value>9fdb557d-2e2f-4fe5-a193-e1cf8cf49bc4</value>
</change>
```

Which removes a name with ID : 9fdb557d-2e2f-4fe5-a193-e1cf8cf49bc4 from the patient's name list then replaces it.

You can also patch using JSON, for example, the following patch will remove the tag "favoriteColour" and replace it:

```javascript
{
    "$type": "Patch",
    "appliesTo": {
        "type": "Patient",
        "id": "9fdb557d-2e2f-4fe5-a193-e1cf8cf49bc4"
    },
    "change": [
        {
            "$type": "PatchOperation",
            "path": "tag",
            "op": "Remove",
            "value": {
                "$type": "EntityTag",
                "key": "favoriteColor"
            }
        },
        {
            "$type": "PatchOperation",
            "path": "tag",
            "op": "Add",
            "value": {
                "$type": "EntityTag",
                "key": "favoriteColor",
                "value": "Blue"
            }
        }
    ]
}                
```

### Dealing with Conflicts

You can assert that particular values are present or true prior to performing your patch, additionally the SanteDB service will assert on the etag of the `If-Match` header. For example, this patch will change the gender of the patient from MALE to FEMALE, but will only succeed if the etag matches `e15be5a372b742ccac35518df7c9a784` and the gender is currently MALE.

```http
PATCH /hdsi/Patient/9fdb557d-2e2f-4fe5-a193-e1cf8cf49bc4 HTTP/1.1
If-Match: e15be5a372b742ccac35518df7c9a784
Content-Type: application/json

{
    "$type": "Patch",
    "appliesTo": {
        "type": "Patient",
        "id": "9fdb557d-2e2f-4fe5-a193-e1cf8cf49bc4"
    },
    "change": [
        {
            "$type": "PatchOperation",
            "op": "Test",
            "path": "genderConcept",
            "value": "f4e3a6bb-612e-46b2-9f77-ff844d971198"
        },
        {
            "$type": "PatchOperation",
            "path": "genderConcept",
            "op": "Replace",
            "value": "094941e9-a3db-48b5-862c-bc289bd7f86c"
        }
    ]
}             
```

If the server does not have the same copy of the patient, then an HTTP 409 \(CONFLICT\) is returned to the caller. 

You may override \(or force\) the patch to occur by using these sets of headers:

```http
PATCH /hdsi/Patient/9fdb557d-2e2f-4fe5-a193-e1cf8cf49bc4
If-Match: e15be5a372b742ccac35518df7c9a784
Content-Type: application/json
X-Patch-Force: true
```

Which will bypass the outcomes of checks.

{% hint style="info" %}
It is best practice to not append the X-Patch-Force header **unless** a human is indicating that they would like to force the the patch to succeed.
{% endhint %}

### Difference Operation

You can submit an object to the SanteDB API to get a "diff" of two objects. This operation is invoked using the `$diff` operation on the desired instance of the type. For example, to see the instructions it would take to turn patent `9fdb557d-2e2f-4fe5-a193-e1cf8cf49bc4` to `1c8c9aa3-abb8-48ee-992d-8f0c524ce40c` submitting the following request.

```http
POST /hdsi/Patient/9fdb557d-2e2f-4fe5-a193-e1cf8cf49bc4/$diff HTTP/1.1
Content-Type: application/json

{
    "$type":"ApiOperationParameterCollection",
    "parameter": [
        {
            "name":"other",
            "value": "1c8c9aa3-abb8-48ee-992d-8f0c524ce40c"
        }
    ]
}
```



