## .NET 6 SDK

1. Uninstall any .NET 6 versions and workload previews using this script:  
   https://github.com/Redth/dotnet-maui-check/blob/main/Clean-Old-DotNet6-Previews.ps1  
   This is just in case maui-check installed an conflicting version some time ago. You won't be able to uninstall version installed by VS, but this is fine to ignore. It is more to remove the versions before preview 7.
1. Install .NET 6 RC 1  
   Win: https://dotnetcli.azureedge.net/dotnet/Sdk/6.0.0-rc.2.21462.1/dotnet-sdk-6.0.0-rc.2.21462.1-win-x64.exe   
   macOS: https://dotnetcli.azureedge.net/dotnet/Sdk/6.0.0-rc.2.21462.1/dotnet-sdk-6.0.0-rc.2.21462.1-osx-x64.pkg  

## Android/iOS Prerequisites

iOS will require Xcode 13 beta 5. You can get this [here](https://developer.apple.com/download/more/?name=Xcode).

Android API-31 (Android 12) is now the default in .NET 6 rc1.

To install go to `Tools` > `Android` > `Android SDK Manager`:

![SDK Manager](images/API-31.png)

You may need to enable all sources as well:

![SDK Manager](images/SDK-Manager-Sources.png)

## .NET MAUI Workload

1. Install the workloads individually: `android-aot`, `ios`, `maccatalyst`, `macos`, `tvos`  
   This is due to this bug: https://github.com/dotnet/sdk/issues/19739  
   Use the source: `--source https://aka.ms/dotnet/maui/main/index.json`
1. Install maui: `dotnet workload install maui --source https://aka.ms/dotnet/maui/main/index.json`
1. Make sure to **remove all previous** Reunion extensions and install the new one:  
   https://marketplace.visualstudio.com/items?itemName=ProjectReunion.MicrosoftSingleProjectMSIXPackagingToolsDev17

You'll probably need to run these commands with elevated privileges.

## Building Apps

Create new projects via `dotnet new maui` or the .NET MAUI template in Visual Studio 2022.

Until .NET 6 RC1 release day, you will need a `nuget.config` file such as:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <packageSources>
    <add key="dotnet6" value="https://pkgs.dev.azure.com/dnceng/public/_packaging/dotnet6/nuget/v3/index.json" />
  </packageSources>
</configuration>
```
