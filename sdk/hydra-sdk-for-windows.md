---
description: >-
  This is the SDK targeting .NET Framework 4.5 that helps to easily develop
  Windows application with required Hydra custom VPN protocol support.
---

# Hydra SDK for Windows

Download [the last version SDK](https://firebasestorage.googleapis.com/v0/b/web-portal-for-partners.appspot.com/o/products%2FHydraSDK_Win_version_1.4.0.262_partnerapi_1.0.3.56_with_TAP_signed.zip?alt=media&token=518f7daa-d498-40ac-a4b6-21af862b8be5)

## Requirements

* Windows 7 or later
* .NET Framework 4.5

## Files

* HydraExecutable\x32bit\afvpn.dll
* HydraExecutable\x32bit\hydra.exe 
* HydraExecutable\x64bit\afvpn.dll
* HydraExecutable\x64bit\hydra.exe
* TapDriver\x32\AFTap.inf
* TapDriver\x32\aftap0901.cat
* TapDriver\x32\aftap0901.sys
* TapDriver\x32\OemVista.inf
* TapDriver\x32\tap0901.cat
* TapDriver\x32\tap0901.sys
* TapDriver\x32\tapinstall.exe
* TapDriver\x64\AFTap.inf
* TapDriver\x64\aftap0901.cat
* TapDriver\x64\aftap0901.sys
* TapDriver\x64\OemVista.inf
* TapDriver\x64\tap0901.cat
* TapDriver\x64\tap0901.sys
* TapDriver\x64\tapinstall.exe
* afvpn.manifest
* afvpn.tlb
* Foundation.ExtProc.Hydra.ComTypes.dll
* Hydra.Sdk.Windows.dll
* Hydra.Sdk.Windows.Service.exe
* Microsoft.Practices.ServiceLocation.dll
* Microsoft.Practices.Unity.Configuration.dll
* Microsoft.Practices.Unity.dll
* Microsoft.Practices.Unity.RegistrationByConvention.dll
* Newtonsoft.Json.dll
* PartnerApi.dll
* SimpleWifi.dll
* System.Buffers.dll
* System.Collections.Immutable.dll
* System.Memory.dll
* System.Runtime.CompilerServices.Unsafe.dll
* System.Threading.Tasks.Extensions.dll
* System.ValueTuple.dll

## Preconditions

### TAP driver installation

TAP driver installation requires administrator permissions. For windows 7, 8 and 8.1 execute the following command:

```text
tapinstall.exe install AFTap.inf aftap0901
```

and for Windows 10:

```text
tapinstall.exe install OemVista.inf tap0901
```

### Windows service installation

To be able to use the hydra service you need to install it into the system once. It could be done by the following command:

```text
Hydra.Sdk.Windows.Service.exe -install <serviceName>
```

where `serviceName` is the name of your service.

## Working with Hydra SDK

### References

Your project have to reference next libraries:

* Hydra.Sdk.Windows.dll
* PartnerApi.dll

There is no need to reference other files, but they should be located in the same directory keeping file structure for a sub-folder named `HydraExecutable`.

### Initialization

Before you can use Hydra SDK in your application you have to initialize it:

```csharp
var backendConfiguration = new BackendServerConfiguration(CarrierId, BackendAddress, DeviceId);
var hydraConfiguration = new HydraWindowsConfiguration(ServiceName, new Dictionary<int, IConnectionRule>());
var hydraBootstrapper = new HydraWindowsBootstrapper();
hydraBootstrapper.Bootstrap(backendConfiguration, hydraConfiguration);
```

`CarrierId` is your project id from the developer

`BackendAddress` is URL address to work with our backend.

`DeviceId` is a unique identifier of an application installation. **NOTE:** you can use anything as an ID, but it must be unique for your carrier.

### Authentication

There two ways how you can login. The first one is anonymous:

```csharp
var hydraSdk = HydraIoc.Container.Resolve<IHydraSdk>();
var loginResponse = await hydraSdk.Login(CarrierId, AuthMethod.Anonymous()).ConfigureAwait(false);
```

The second one is OAuth2. If you have your custom OAuth2 service:

```csharp
var hydraSdk = HydraIoc.Container.Resolve<IHydraSdk>();
varloginResponse = await hydraSdk.Login(CarrierId, AuthMethod.Custom("OAuth2-token", "your_method")).ConfigureAwait(false);
```

Also, the SDK supports 3d-party token providers:

```csharp
AuthMethod.Facebook("OAuth2-token");
AuthMethod.Firebase("OAuth2-token");
AuthMethod.GitHub("OAuth2-token");
AuthMethod.Google("OAuth2-token");
```

An example of login implementation:

```csharp
var hydraSdk = HydraIoc.Container.Resolve<IHydraSdk>();

var authMethod = AuthMethod.Firebase(token);
var result = await hydraSdk.Login(authMethod).ConfigureAwait(false);

if (!loginResponse.IsSuccess)
{
    // Handle login error
}
else
{
    // Handle successful login 
}
```

### Connection

After a successful login, you can start a VPN connection, but first you have to get available VPN nodes. An example of connect implementation:

```text
var loginResponse = await hydraSdk.Login(CarrierId, AuthMethod.Anonymous()).ConfigureAwait(false);
var carrier = new Carrier(CarrierId, CarrierId, loginResponse.AccessToken);
var nodes = await hydraSdk.GetNodes(carrier).ConfigureAwait(false);
var firstOrDefault = nodes.VpnCountries.FirstOrDefault(x => x.CountryCode == "us");
await hydraSdk.StartVpn(firstOrDefault).ConfigureAwait(false);
```

To stop the connection:

```text
await hydraSdk.StopVpn().ConfigureAwait(false);
```

### Events

#### `VpnConnectionStateChanged`

Occurs when the SDK changes its state. `ConnectionStateChangedEventArgs` contains two properties:

`VpnConnectionState State` is the current state of the SDK. Possible values are:

* `Disconnected`
* `Connected`
* `Connecting`
* `Disconnecting`

`bool IsError` is a flag that shows if the state was changed because of an error. Can be `true` only for `Disconnected` state.

#### `StatisticsChanged`

Occurs when the SDK detects traffic counter changes on the client side. `VpnStatisticsChangedEventArgs` contains one property `VpnStatistics Data` with two metrics:

* `long BytesSent`
* `long BytesReceived`

## Setting up logging

Key places of Hydra SDK are instrumented with logging for debug purposes. If you need to see those log messages, you have to provide your own `LoggerListener`.

First, create class derived from `BaseLoggerListener` and implement abstract methods:

```text
internal class MyLoggerListener : BaseLoggerListener
{
    public override void Trace(string message)
    {
        Console.WriteLine(message);    
    }

    // Here goes implementation of other methods
}
```

Then add an instance of your logger listener as handler to the HydraLogger:

```text
HydraLogger.AddHandler(new MyLoggerListener());
```

That's all. You will get log output of your logger.

## Console application example

```text
namespace ConsoleVPN
{
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Threading.Tasks;
    using Hydra.Sdk.Windows;
    using Hydra.Sdk.Windows.IoC;
    using Hydra.Sdk.Windows.Misc;
    using Hydra.Sdk.Windows.Network.Rules;
    using PartnerApi.Model.Nodes;

    internal class Program
    {
        private const string CarrierId = "afdemo";
        private const string ServiceName = "Cool VPN Service";
        private const string BackendAddress = "	https://backend.northghost.com/";
        private const string DeviceId = "7B5E3123-C7AD-4EC8-8F81-6D46005DABA7";

        private static IHydraSdk hydraSdk;

        private static async Task Main(string[] args)
        {
            var backendConfiguration = new BackendServerConfiguration(CarrierId, BackendAddress, DeviceId);
            var hydraConfiguration = new HydraWindowsConfiguration(ServiceName, new Dictionary<int, IConnectionRule>());
            var hydraBootstrapper = new HydraWindowsBootstrapper();
            hydraBootstrapper.Bootstrap(backendConfiguration, hydraConfiguration);
            hydraSdk = HydraIoc.Container.Resolve<IHydraSdk>();

            var loginResponse = await hydraSdk.Login(CarrierId, AuthMethod.Anonymous()).ConfigureAwait(false);
            var carrier = new Carrier(CarrierId, CarrierId, loginResponse.AccessToken);
            var nodes = await hydraSdk.GetNodes(carrier).ConfigureAwait(false);
            var firstOrDefault = nodes.VpnCountries.FirstOrDefault(x => x.CountryCode == "us");
            await hydraSdk.StartVpn(firstOrDefault).ConfigureAwait(false);

            hydraSdk.VpnConnectionStateChanged += (s, e) => { Console.WriteLine(e.State); };
            hydraSdk.StatisticsChanged += (s, e) => { Console.WriteLine($"Received: {e.Data.BytesReceived} | Sent: {e.Data.BytesSent}"); };

            var key = Console.ReadKey();

            if (key.Key == ConsoleKey.Escape)
            {
                await hydraSdk.StopVpn().ConfigureAwait(false);
            }
        }
    }
}
```

