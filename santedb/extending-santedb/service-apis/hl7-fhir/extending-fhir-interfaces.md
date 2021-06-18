# Extending FHIR Interfaces

The SanteDB FHIR subsystem allows developers to easily add new behaviours, resources, and operations. The following extension points and interfaces are exposed in the SanteDB FHIR package:

* Message Operations \(IFhirMessageOperation\) - Used to add new FHIR message operations into the SanteDB stack \(i.e. on the $process-message interface\)
* Operations \(IFhirOperationHandler\) - Used to add new FHIR operations invoked using `$operationName` 
* Custom Extensions \(IFhirExtensionHandler\) - Used to add/expose individual extensions on the existing endpoints and messages. 
* Behavior Modifier \(IFhirRestBehaviorModifier\) - Used to intercept operations on the FHIR interface and modify the behaviour of the call.
* Profile / Validation \(IFhirProfileValidationHandler\) - Used to perform validation on any resource which is created/updated. This is typically used on the $validate message.

## Message Operations

[FHIR Messaging](https://www.hl7.org/fhir/messaging.html) allows for complex operations to be invoked using a `Bundle` which contains a MessageHeader resource. For example, in order to implement an operation HelloWorld , a FHIR message may contain:

```javascript
{
  "resourceType": "Bundle",
  "type": "message",
  "entry": [
    {
      "fullUrl": "MessageHeader/example-1",
      "resource": {
        "resourceType": "MessageHeader",
        "id": "example-1",
        "eventUri": "urn:hello:world",
        "source": {
          "endpoint": "http://ohie.org/test/harness"
        },
        "focus": [
          {
            "reference": "Parameters/example-1"
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
      "fullUrl": "Parameters/example-1",
      "resource": {
        "resourceType": "Parameters",
        "parameter": [
          {
            "name": "your-name",
            "valueString": "Bob!"
          }
        ]
      }
    }
  ]
}
```

Given the contrived example above, you can register a new IFhirMessageOperation to be invoked when the operation `urn:hello:world` message trigger you would implement a handler.

```csharp
/// <summary>
/// A sample FHIR operation for Hello World
/// </summary>
public class HelloWorldOperation : IFhirMessageOperation
{
    /// <summary>
    /// The event URI which this operation should be invoked
    /// </summary>
    public Uri EventUri => new Uri("urn:hello:world");

    /// <summary>
    /// Actually perform the operation
    /// </summary>
    /// <param name="requestHeader">The FHIR MessageHeader which was in the original request</param>
    /// <param name="entries">The entries in the focus of the message header</param>
    /// <returns>The result of the operation</returns>
    public Resource Invoke(MessageHeader requestHeader, params Bundle.EntryComponent[] entries)
    {
         // Do Hello World Stuff Here
    }
 }
```

### Registering your Message Handler

Finally, SanteDB does not automatically enable all operations, therefore it is required to register your operation handler in the messages portion of the FHIR configuration section.

```markup
<section xsi:type="FhirServiceConfigurationSection" restEndpoint="FHIR" >
    <messages>
      <add>urn:hello:world</add>
    </messages>
  </section>
```

## Rest Operations

REST operations are invoked using the GET or POST method on a scoped resource. Typically the invoke is in the form: `http://example.com/fhir/Patient/$operation` . FHIR REST operations can be registered with an implementation of IFhirOperationHandler , for example, a FHIR operation for hello-world may be called as `GET http://example.com/fhir/Patient/$hello-world`. 

To implement the `hello-world` operation, a C\# class is written.

```csharp
/// <summary>
/// IHE PIXm Operation
/// </summary>
public class HelloWorldOperation : IFhirOperationHandler
{

    /// <summary>
    /// Gets the name of the operation on the URL
    /// </summary>
    public string Name => "hello-world";

    /// <summary>
    /// Gets the URI of the operation which is exposed in the CapabilityStatement
    /// </summary>
    public Uri Uri => new Uri("http://example.com/fhir/hello-world");

    /// <summary>
    /// Applies to which resources (returning an empty array indicates this is a system operation)
    /// </summary>
    public ResourceType[] AppliesTo => new ResourceType[] { ResourceType.Patient };

    /// <summary>
    /// Called when a GET or POST is executed against the URL
    /// </summary>
    /// <param name="parameters">The parameters object passed (if the operation was a POST)</param>
    /// <returns>The resource representing the result of the operation</returns>
    public Resource Invoke(Parameters parameters) {
        // Do Hello World FHIR Stuff
    }
}
```

Finally, SanteDB does not automatically enable all operations, therefore it is required to register your operation handler in the messages portion of the FHIR configuration section.

```markup
<section xsi:type="FhirServiceConfigurationSection" restEndpoint="FHIR" >
    <operations>
      <add>hello-world</add>
    </operations>
  </section>
```

## Extension Handlers

By default, SanteDB's internal properties are mapped to FHIR base resources, and this is handled through the `DataTypeConverter` class. You may, however, have a need to expose additional data, relationships, or receive them. This can be done by using [FHIR Extensions](https://www.hl7.org/fhir/extensibility-registry.html). 

FHIR Extension handlers are implemented using the IFHirExtensionHandler interface. For example, if you wanted to implement an extension handler which tags a patient if the value of the extension is a certain value.

{% hint style="info" %}
If the data you are capturing in your extension is registered as a [SanteDB extension](../../../architecture/data-and-information-architecture/extended-data.md) in the RIM the FHIR handler will automatically map these to an extension in FHIR.
{% endhint %}

```csharp
/// <summary>
/// FHIR Extension Handler 
/// </summary>
/// <remarks>
/// This interface is used when processing resources to/from FHIR and allow
/// custom FHIR extensions to map data from extensions into the underlying 
/// objects in the CDR schema.
/// </remarks>
public class FavoriteColorExtensionHandler : IFhirExtensionHandler
{

    /// <summary>
    /// Gets the URI of the extension which appears within a resource
    /// </summary>
    public Uri Uri => new Uri("http://example.com/fhir/extensions/reviewState");

    /// <summary>
    /// Gets the URI of the profile that this extension is defined in 
    /// which is exposed on the profile definition.
    /// </summary>
    public Uri ProfileUri => new Uri("http://example.com/fhir/profiles/example");
    
    /// <summary>
    /// Gets the resource type that this applies to (or null if it applies to all types)
    /// </summary>
    public ResourceType? AppliesTo => ResourceType.Patient;

    /// <summary>
    /// Before returning the model object to the caller this method is called
    /// so that your extension handler can construct the FHIR Extension
    /// </summary>
    /// <param name="modelObject">The object that was loaded from the database which you can use to load data for your extension</param>
    /// <returns>The constructed FHIR extension</returns>
    public Extension Construct(IIdentifiedEntity modelObject) {
        if(modelObject is IHasStatus status) {
            if(status.StatusConceptKey == StatusKeys.New) {
                return new Extension() {
                    Url = this.Uri.ToString(),
                    Value = "not-reviewed"
                }
            }
        }
        return null;
    }

    /// <summary>
    /// Parse the specified extension from FHIR and update the <paramref name="modelObject"/> accordingly
    /// </summary>
    /// <param name="fhirExtension">The FHIR Extension to parsed</param>
    /// <param name="modelObject">The current model object into which the extension data should be added</param>
    /// <returns>True if the extension was parsed successfully</returns>
    public bool Parse(Extension fhirExtension, IdentifiedData modelObject) {
          if(modelObject is IHasStatus status) {
              if(fhirExtension.Value == "not-reviewed") {
                  status.StatusConceptKey = StatusKeys.New;
              } else {
                  status.StatusConceptKey = StatusKeys.Active;
              }
          }
    }

}
```

Finally, SanteDB does not automatically enable all extensions, therefore it is required to register your extension handler in the messages portion of the FHIR configuration section.

```markup
<section xsi:type="FhirServiceConfigurationSection" restEndpoint="FHIR" >
    <extensions>
      <add>http://example.com/fhir/extensions/reviewState</add>
    </extensions>
  </section>
```

