`IUpstreamIntegrationService` in assembly SanteDB.Core.Api version 3.0.1980.0

# Summary
Represents an integration service which is responsible for sending and
            pulling data to/from remote sources as a configured device or application account principal 
            rather than an interactive user

# Events

|Event|Type|Description|
|-|-|-|
|Responding|EventHandler&lt;RestResponseEventArgs>|Fired on response|
|ProgressChanged|EventHandler&lt;ProgressChangedEventArgs>|Progress has changed|
|Responded|EventHandler&lt;UpstreamIntegrationResultEventArgs>|The remote system has responsed|

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Query|IResourceCollection|*Type* **modelType**<br/>*Expression* **filter**<br/>*UpstreamIntegrationQueryControlOptions* **options**|Find the specified filtered object|
|Query|IResourceCollection|*Expression&lt;Func&lt;TModel,Boolean>>* **predicate**<br/>*UpstreamIntegrationQueryControlOptions* **options**|Instructs the integration service to locate a specified object(s)|
|Get|IdentifiedData|*Type* **modelType**<br/>*Guid* **key**<br/>*Nullable&lt;Guid>* **versionKey**<br/>*UpstreamIntegrationQueryControlOptions* **options**|Instructs the integration service to retrieve the specified object|
|HarmonizeTemplateId|IHasTemplate|*IHasTemplate* **iht**|Harmonizes the template identifier information on  with the upstream's template definition|
|Get|TModel|*Guid* **key**<br/>*Nullable&lt;Guid>* **versionKey**<br/>*UpstreamIntegrationQueryControlOptions* **options**|Gets a specified model.|
|Insert|void|*IdentifiedData* **data**|Inserts specified data.|
|Obsolete|void|*IdentifiedData* **data**<br/>*Boolean* **forceObsolete**|Obsoletes specified data.|
|Update|void|*IdentifiedData* **data**<br/>*Boolean* **forceUpdate**<br/>*Boolean* **autoResolveConflict**|Updates specified data.|
|AuthenticateAsDevice|IPrincipal|*IPrincipal* **onBehalfOf**|Authenticate as the device|
|Invoke|Object|*Type* **modelType**<br/>*String* **operation**<br/>*ParameterCollection* **parameters**|Invoke an operation on the remote service|

# Implementations


## DefaultUpstreamIntegrationService - (SanteDB.Client)
An upstream integration service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Client.Upstream.Management.DefaultUpstreamIntegrationService, SanteDB.Client, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyUpstreamIntegrationService : SanteDB.Core.Services.IUpstreamIntegrationService { 
	public String ServiceName => "My own IUpstreamIntegrationService service";
	/// <summary>
	/// Fired on response
	/// </summary>
	public event EventHandler<RestResponseEventArgs> Responding;
	/// <summary>
	/// Progress has changed
	/// </summary>
	public event EventHandler<ProgressChangedEventArgs> ProgressChanged;
	/// <summary>
	/// The remote system has responsed
	/// </summary>
	public event EventHandler<UpstreamIntegrationResultEventArgs> Responded;
	/// <summary>
	/// Find the specified filtered object
	/// </summary>
	public IResourceCollection Query(Type modelType,Expression filter,UpstreamIntegrationQueryControlOptions options){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Instructs the integration service to locate a specified object(s)
	/// </summary>
	public IResourceCollection Query<TModel>(Expression<Func<TModel,Boolean>> predicate,UpstreamIntegrationQueryControlOptions options){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Instructs the integration service to retrieve the specified object
	/// </summary>
	public IdentifiedData Get(Type modelType,Guid key,Nullable<Guid> versionKey,UpstreamIntegrationQueryControlOptions options){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Harmonizes the template identifier information on  with the upstream's template definition
	/// </summary>
	public IHasTemplate HarmonizeTemplateId(IHasTemplate iht){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets a specified model.
	/// </summary>
	public TModel Get<TModel>(Guid key,Nullable<Guid> versionKey,UpstreamIntegrationQueryControlOptions options){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Inserts specified data.
	/// </summary>
	public void Insert(IdentifiedData data){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Obsoletes specified data.
	/// </summary>
	public void Obsolete(IdentifiedData data,Boolean forceObsolete){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Updates specified data.
	/// </summary>
	public void Update(IdentifiedData data,Boolean forceUpdate,Boolean autoResolveConflict){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Authenticate as the device
	/// </summary>
	public IPrincipal AuthenticateAsDevice(IPrincipal onBehalfOf){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Invoke an operation on the remote service
	/// </summary>
	public Object Invoke(Type modelType,String operation,ParameterCollection parameters){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IUpstreamIntegrationService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IUpstreamIntegrationService.htm)
* [DefaultUpstreamIntegrationService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Client_Upstream_Management_DefaultUpstreamIntegrationService.htm)
