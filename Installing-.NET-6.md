## .NET 6 SDK

In most cases, when you have Visual Studio installed with the .NET workloads checked, these steps are not required.

1. Install the latest .NET 6:  
   - [Win (x64)](https://aka.ms/dotnet/6.0.1xx/daily/dotnet-sdk-win-x64.exe)   
   - [macOS (x64)](https://aka.ms/dotnet/6.0.1xx/daily/dotnet-sdk-osx-x64.pkg)  
   - [macOS (arm64)](https://aka.ms/dotnet/6.0.1xx/daily/dotnet-sdk-osx-arm64.pkg)
2. Add this to your NuGet.config:  
   ```xml
    <add key="darc-pub-dotnet-runtime" value="https://pkgs.dev.azure.com/dnceng/public/_packaging/darc-pub-dotnet-runtime-6f411658/nuget/v3/index.json"  />
    <add key="dotnet6" value="https://aka.ms/dotnet6/nuget/index.json" />
    ```
   > NOTE: this is going to contain the "stable" versions of the packages, so you will have to clear the NuGet cache when this feed changes and when .NET ships. The various `darc-pub-dotnet-*` feeds are temporary and are generated on various builds. These feeds my disappear and be replaced with new ones as new builds come out. Make sure to verify that you are on the latest here and clear the nuget cache if it changes:  
   > `dotnet nuget locals all --clear`

## .NET MAUI Workload

> You'll probably need to run these commands with elevated privileges.

Install the .NET MAUI workload using the versions from a particular branch:  

For example, the "preview.10" branch:
```
dotnet workload install maui `
   --from-rollback-file https://aka.ms/dotnet/maui/preview.10.json `
   --source https://aka.ms/dotnet6/nuget/index.json `
   --source https://pkgs.dev.azure.com/dnceng/public/_packaging/darc-pub-dotnet-runtime-6f411658/nuget/v3/index.json `
   --source https://pkgs.dev.azure.com/dnceng/public/_packaging/darc-pub-dotnet-emsdk-1ec2e17f/nuget/v3/index.json
```


Or, the "main" branch:
```
dotnet workload install maui `
   --from-rollback-file https://aka.ms/dotnet/maui/main.json `
   --source https://aka.ms/dotnet6/nuget/index.json `
   --source https://pkgs.dev.azure.com/dnceng/public/_packaging/darc-pub-dotnet-runtime-6f411658/nuget/v3/index.json `
   --source https://pkgs.dev.azure.com/dnceng/public/_packaging/darc-pub-dotnet-emsdk-1ec2e17f/nuget/v3/index.json
```  

For the latess release, there is preview.9:

```
dotnet workload install maui `
   --from-rollback-file https://aka.ms/dotnet/maui/preview.9.json `
   --source https://api.nuget.org/v3/index.json
```

If you are building maui yourself, then you probably want all the workloads:

```
dotnet workload install android ios maccatalyst tvos macos maui wasm-tools `
   --from-rollback-file https://aka.ms/dotnet/maui/main.json `
   --source https://aka.ms/dotnet6/nuget/index.json `
   --source https://pkgs.dev.azure.com/dnceng/public/_packaging/darc-pub-dotnet-runtime-6f411658/nuget/v3/index.json `
   --source https://pkgs.dev.azure.com/dnceng/public/_packaging/darc-pub-dotnet-emsdk-1ec2e17f/nuget/v3/index.json
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

**Troubleshooting**

Uninstall any .NET 6 versions and workload previews using this script:  

   https://github.com/Redth/dotnet-maui-check/blob/main/Clean-Old-DotNet6-Previews.ps1  
   > This is just in case maui-check installed an conflicting version some time ago. You won't be able to uninstall version installed by VS, but this is fine to ignore. It is more to remove the versions before preview 7.