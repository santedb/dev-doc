`IPeerToPeerShareService` in assembly SanteDB.Client version 3.0.1980.0

# Summary
Represents a peer to peer sharing service which allows the host to share data between one or more hosts via an appropriate protocol

## Description
This should use the native operating system's BlueTooth operation for data transfer over bluetooth.

# Events

|Event|Type|Description|
|-|-|-|
|Received|EventHandler&lt;PeerToPeerDataEventArgs>|Fired after the data transfer has completed|
|Receiving|EventHandler&lt;PeerToPeerEventArgs>|Fired when the data transfer is about to begin|
|Sent|EventHandler&lt;PeerToPeerDataEventArgs>|Fired when the data has been sent|
|Sending|EventHandler&lt;PeerToPeerDataEventArgs>|Fired when the data is about to be sent|

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Send|IdentifiedData|*String* **recipient**<br/>*IdentifiedData* **entity**|Send the specified entity to the remote host|
|GetRecipientList|IEnumerable&lt;String>|*none*|TODO|

# Implementations

None

# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Client.Services;
/// Other usings here
public class MyPeerToPeerShareService : SanteDB.Client.Services.IPeerToPeerShareService { 
	public String ServiceName => "My own IPeerToPeerShareService service";
	/// <summary>
	/// Fired after the data transfer has completed
	/// </summary>
	public event EventHandler<PeerToPeerDataEventArgs> Received;
	/// <summary>
	/// Fired when the data transfer is about to begin
	/// </summary>
	public event EventHandler<PeerToPeerEventArgs> Receiving;
	/// <summary>
	/// Fired when the data has been sent
	/// </summary>
	public event EventHandler<PeerToPeerDataEventArgs> Sent;
	/// <summary>
	/// Fired when the data is about to be sent
	/// </summary>
	public event EventHandler<PeerToPeerDataEventArgs> Sending;
	/// <summary>
	/// Send the specified entity to the remote host
	/// </summary>
	public IdentifiedData Send(String recipient,IdentifiedData entity){
		throw new System.NotImplementedException();
	}
	public IEnumerable<String> GetRecipientList(){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IPeerToPeerShareService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Client_Services_IPeerToPeerShareService.htm)
