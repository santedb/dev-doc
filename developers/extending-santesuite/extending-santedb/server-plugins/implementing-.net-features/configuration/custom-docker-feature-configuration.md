# Custom Docker Feature Configuration

SanteDB typically uses the configuration file and the `IFeature` mechanism for advanced configurations. However, SanteDB also runs within Docker and Kubernetes environments. These are configured using the `IDockerFeature` interface.&#x20;

For example, to expose `FOO` as a feature on the `SDB_FEATURE` and provide a parameter called `BAR` which is leveraging the application settings part of the configuration file:

```csharp
/// <summary>
/// A sample docker feature
/// </summary>
public class FooDockerFeature : IDockerFeature
{

    public const string FooBarSetting = "BAR";

    /// <summary>
    /// This is the feature ID on the SDB_FEATURE
    /// </summary>
    public string Id => "FOO";

    /// <summary>
    /// Settings for the foobar feature
    /// </summary>
    public IEnumerable<string> Settings => new String[] { FooBarSetting };

    /// <summary>
    /// Configure this service
    /// </summary>
    public void Configure(SanteDBConfiguration configuration, IDictionary<string, string> settings)
    {

        // We can fetch the settings for our feature (parsed from docker 
        // environment) with the settings parameter
        if (!settings.TryGetValue(FooBarSetting, out string fooBar))
        {
            fooBar = "Hello World!";
        }
        
        // Set my settings
        configuration.AddSection(new FooBarConfigurationSection() {
            Bar = fooBar
        });
        
        // Add foobar services
        var serviceConfiguration = configuration.GetSection<ApplicationServiceContextConfigurationSection>().ServiceProviders;
        serviceConfiguration.Add(new TypeReferenceConfiguration(typeof(FooBarService)));
    }
}
```
