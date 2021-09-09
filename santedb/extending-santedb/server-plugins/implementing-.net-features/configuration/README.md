# Configuration

SanteDB provides a portable configuration system which is used by the iCDR and dCDR on any platform in which SanteDB is running. 

{% hint style="warning" %}
SanteDB may be configured to load configuration from a central cluster service, or load configurations from databases, the file system, or unit testing context. It is highly recommended you use the SanteDB.Core.Configuration interfaces rather than the System.Configuration namespaces.
{% endhint %}

## Configuration Manager

The configuration is managed by the IConfigurationManager service, this service provides methods for loading connection strings, app settings, and structured configuration sections. 

### App Settings

The most basic form of configuration provided by the configuration manager is the app settings properties. App settings are key/value pairs contained within the configuration source which can be used for storing and retrieving simple settings, for example:

```csharp
public void MyFunction() {
    var configMgr = ApplicationServiceContext.Current.GetService<IConfigurationManager>();
    
    // Get the user's app setting for a preference
    var fooSetting = configMgr.GetAppSetting("foo");
    if(String.IsNullOrEmpty(fooSetting))
        configMgr.SetAppSetting("foo","bar"); // Sets app setting foo to bar
}    
```

### Connection Strings

Connection strings provide connection details to/from data sources in the SanteDB application context. Connection strings can be used in conjunction with the SanteDB.OrmLite library or any other database provider. For example:

```csharp
public void MyDatabaseFunction() {
    var configMgr = ApplicationServiceContext.Current.GetService<IConfigurationManager>();
    
    // Get the connection string for MainDatabase
    var connectionString = configMgr.GetConnectionString("MainDatabase");
    if(connectionString == null)
        throw new InvalidOperationException("Cannot find main database!");
    
    // Retrieves server and port from connection string
    // server=foo;port=5432;pooling=true
    string server = connectionString.GetComponent("server"),
        port = connectionString.GetComponent("port");
}
```



## Configuration Sections

It is often the case that modules must not use hard coded values, and must allow for some degree of user configuration. The use of the `GetAppSetting` / `SetAppSetting` may be appropriate for simple settings, however for more complex configuration you should define your own IConfigurationSection implementation.

A configuration section is a complex structure contained within the configuration provider. Depending on the configuration provider it may store these values in JSON, XML, a database, or other appropriate format.

### Defining a Configuration Section

Configuration sections are defined by implementing the IConfigurationSection interface, this class should be XML Serializable and should contain all of the settings. For example, if we want to write a simple HelloWorldConfigurationSection which stores a name and a few other properties:

```csharp
[XmlType(nameof(HelloWorldConfigurationSection), Namespace = "http://foo.bar")]
public sealed class HelloWorldConfigurationSection : IConfigurationSection
{
    
    [XmlArray("names"), XmlArrayItem("add")]
    public List<string> Names { get; set; }
    
    [XmlElement("nHello")]
    public int NumberOfTimes { get; set; }
}
```

When you deploy your service, you can configure it using whatever configuration technology the configuration manager leverages. By default, most SanteDB instances use an XML file named `SanteDB.config.xml` . To express the configuration above in that file, you must first register your configuration type:

```markup
<SanteDBConfiguration xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xmlns="http://santedb.org/configuration" 
        xmlns:hello="http://foo.bar">
  <sections>
    <add type="HelloWorld.HelloWorldConfigurationSection, HelloWorld, Version=1.0.0.0" />
```

Since our configuration section is defined in the http://foo.bar namespace we have to declare the namespace in the XML file, if we were using the default namespace this definition could be ignored.

Next, we need to add our actual configuration section to the file, this is done with the &lt;section&gt; attribute:

```markup
<section xsi:type="hello:HelloWorldConfigurationSection">
    <names>
        <add>Joe</add>
        <add>Bob</add>
    </names>
    <nHello>20</nHello>
</section>
```

### Consuming a Configuration Section

Once defined, the configuration section may be consumed by any service where the section class is visible. To retrieve the HelloWorldConfigurationSection for example:

```csharp
public void SayHello() {
    var configMgr = ApplicationServiceContext.Current.GetService<IConfigurationManager>();
    
    var config = configMgr.GetSection<HelloWorldConfigurationSection>();
    
    for(int i = 0; i < config.NumberOfTimes; i++)
        Console.WriteLine(String.Join(";", config.Names));
}
```



