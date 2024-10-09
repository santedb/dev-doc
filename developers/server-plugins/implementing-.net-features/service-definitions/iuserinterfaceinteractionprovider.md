`IUserInterfaceInteractionProvider` in assembly SanteDB.Client version 3.0.1980.0

# Summary
An interface that can provide low level dialogs for confirmations and messages

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Confirm|Boolean|*String* **message**|Shows a confirmation dialog box with|
|Alert|void|*String* **message**|Shows an alert message box to the|
|Prompt|String|*String* **message**<br/>*Boolean* **maskEntry**|Shows a prompt for the user to enter a response|
|SetStatus|void|*String* **taskIdentifier**<br/>*String* **statusText**<br/>*Single* **progressIndicator**|Set the application status bar to to the specified value|

# Implementations


## ConsoleUserInterfaceInteractionProvider - (SanteDB.Client)
An implementation of the [IUserInterfaceInteractionProvider](http://santesuite.org/assets/doc/net/html/T_SanteDB_Client_UserInterface_IUserInterfaceInteractionProvider.htm) which uses the user's console
            as the method of obtaining inputs and raising alerts

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Client.UserInterface.Impl.ConsoleUserInterfaceInteractionProvider, SanteDB.Client, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## TracerUserInterfaceInteractionProvider - (SanteDB.Client)
Trace user interface provider

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Client.UserInterface.Impl.TracerUserInterfaceInteractionProvider, SanteDB.Client, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Client.UserInterface;
/// Other usings here
public class MyUserInterfaceInteractionProvider : SanteDB.Client.UserInterface.IUserInterfaceInteractionProvider { 
	public String ServiceName => "My own IUserInterfaceInteractionProvider service";
	/// <summary>
	/// Shows a confirmation dialog box with
	/// </summary>
	public Boolean Confirm(String message){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Shows an alert message box to the
	/// </summary>
	public void Alert(String message){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Shows a prompt for the user to enter a response
	/// </summary>
	public String Prompt(String message,Boolean maskEntry){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Set the application status bar to to the specified value
	/// </summary>
	public void SetStatus(String taskIdentifier,String statusText,Single progressIndicator){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IUserInterfaceInteractionProvider C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Client_UserInterface_IUserInterfaceInteractionProvider.htm)
* [ConsoleUserInterfaceInteractionProvider C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Client_UserInterface_Impl_ConsoleUserInterfaceInteractionProvider.htm)
* [TracerUserInterfaceInteractionProvider C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Client_UserInterface_Impl_TracerUserInterfaceInteractionProvider.htm)
