## .NET 6 SDK

In most cases, when you have Visual Studio installed with the .NET workloads checked, these steps are not required.

1. OPTIONAL: Uninstall any .NET 6 versions and workload previews using this script:  
   https://github.com/Redth/dotnet-maui-check/blob/main/Clean-Old-DotNet6-Previews.ps1  
   > This is just in case maui-check installed an conflicting version some time ago. You won't be able to uninstall version installed by VS, but this is fine to ignore. It is more to remove the versions before preview 7.
1. OPTIONAL: Install .NET 6:  
   - [Win (x64) 6.0.100-rtm.21514.20](https://dotnetcli.azureedge.net/dotnet/Sdk/6.0.100-rtm.21514.20/dotnet-sdk-6.0.100-rtm.21514.20-win-x64.exe)   
   - [macOS (x64) 6.0.100-rtm.21514.20](https://dotnetcli.azureedge.net/dotnet/Sdk/6.0.100-rtm.21514.20/dotnet-sdk-6.0.100-rtm.21514.20-osx-x64.pkg)  
   - [macOS (arm64) 6.0.100-rtm.21514.20](https://dotnetcli.azureedge.net/dotnet/Sdk/6.0.100-rtm.21514.20/dotnet-sdk-6.0.100-rtm.21514.20-osx-arm64.pkg)

## .NET MAUI Workload

> You'll probably need to run these commands with elevated privileges.

Install the .NET MAUI workload using the versions from a particular branch:  

For example, the "preview.10" branch:
```
dotnet workload install maui `
   --from-rollback-file https://aka.ms/dotnet/maui/preview.10.json `
   --source https://aka.ms/dotnet6/nuget/index.json
```


Or, the "main" branch:
```
dotnet workload update install maui `
   --from-rollback-file https://aka.ms/dotnet/maui/main.json `
   --source https://aka.ms/dotnet6/nuget/index.json
```  

If you are building maui yourself, then you probably want all the workloads:

```
dotnet workload install android ios maccatalyst tvos macos maui wasm-tools `
   --from-rollback-file https://aka.ms/dotnet/maui/main.json `
   --source https://aka.ms/dotnet6/nuget/index.json
```

## Prerequisites

### Windows

Make sure to **remove all previous** Reunion extensions and install the new one:

https://marketplace.visualstudio.com/items?itemName=ProjectReunion.MicrosoftSingleProjectMSIXPackagingToolsDev17

### iOS

iOS will require Xcode 13 beta 5. You can get this [here](https://developer.apple.com/download/more/?name=Xcode).

### Android

Android API-31 (Android 12) is now the default in .NET 6 rc1.

To install go to `Tools` > `Android` > `Android SDK Manager`:

![SDK Manager](images/API-31.png)

You may need to enable all sources as well:

![SDK Manager](images/SDK-Manager-Sources.png)

## Building Apps

Create new projects via `dotnet new maui` or the .NET MAUI template in Visual Studio 2022.

Until .NET 6 releases day, you will need a `nuget.config` file such as:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <packageSources>
    <add key="dotnet6" value="https://aka.ms/dotnet6/nuget/index.json" />
  </packageSources>
</configuration>
```
