---
description: 'This page provides instruction on Unit Testing your C# / .NET SanteDB Plugins'
---

# Unit Testing Framework

### Install SanteDB Server TestFramework

Because many core SanteDB components \(including your service implementations\) will need to be registered with a SanteDB host context, you must first establish an application context. SanteDB provides tools for quickly establishing a TestApplicationContext however this requires installation of the nuget package:

```text
Install-Package SanteDB.Server.TestFramework
```

## Setting up the TestApplicationContext

The TestApplicationContext should be initialized in a common place. Below provides an example of a TestClass which initializes a TestApplicationContext.

```csharp
using SanteDB.Core;
using SanteDB.Core.TestFramework;
using System;
using NUnit.Framework;

namespace MyTest {
    [TestFixture]
    public class MyTestClass
    {
        [Setup]
        public void Initialize() {
            
            // Init test context if needed
            if(ApplicationServiceContext.Current == null)
            {
                // Forces .NET To load the FirebirdSQL API
                var p = FirebirdSql.Data.FirebirdClient.FbCharset.Ascii;
                TestApplicationContext.TestAssembly = typeof(TestOpenHIEPixPdq).Assembly;
                TestApplicationContext.Initialize(TestContext.CurrentContext.TestDirectory);
            }
        }
    }
}
```

You will also need to create an embedded resource in your test assembly named TestConfig.xml which contains the configuration you wish to use for your test:

```markup
<SanteDBConfiguration xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" version="1.33.0.0" xmlns="http://santedb.org/configuration">
  <sections>
    <add type="SanteDB.Core.Configuration.ApplicationServiceContextConfigurationSection, SanteDB.Core.Api, Version=1.11.0.29460, Culture=neutral, PublicKeyToken=null" />
    <add type="SanteDB.Core.Configuration.DiagnosticsConfigurationSection, SanteDB.Core.Api, Version=1.30.0.23443, Culture=neutral, PublicKeyToken=null" />
  </sections>
  <section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
      <add type="SanteDB.Core.Services.Impl.ThreadPoolService, SanteDB.Core, Version=0.6.0.0" />
    </serviceProviders>
  </section>
</SanteDBConfiguration>
```

{% hint style="info" %}
Use the SolutionExplorer and Properties window to set the **Build Action** to **Embedded Resource** and ensure that your TestConfig.xml is placed in the root of your test assembly project.
{% endhint %}

### Unit Tests for Data Services

If your unit test requires accessing or interacting with the SanteDB data store or repository services, you should register the required persistence classes in your TestConfig.xml and inherit from DataTest.

```csharp
using SanteDB.Core;
using SanteDB.Core.TestFramework;
using System;
using NUnit.Framework;

namespace MyTest {
    [TestFixture]
    public class MyTestClass : DataTest
    {
        [Setup]
        public void Initialize() {
            
            // Init test context if needed
            if(ApplicationServiceContext.Current == null)
            {
                // Instructs the TestApplicationContext where to load TestConfig.xml
                TestApplicationContext.TestAssembly = typeof(MyTestClass).Assembly;
                // Initialize
                TestApplicationContext.Initialize(TestContext.CurrentContext.TestDirectory);
            }
        }
    }
}
```

### Execution Environment

If you're using the data persistence services, you will need to ensure that the Visual Studio test runner \(or the NUnit tool\) is running in x64 mode. In Visual Studio, this requires selecting Test -&gt; Processor Architecture -&gt; x64.

![](../../../.gitbook/assets/image%20%28199%29.png)

