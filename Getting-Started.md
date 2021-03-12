## Pre-Requisites

1. Visual Studio 16.9 or newer, or Visual Studio for Mac 8.9 or newer
    1. Mobile and Desktop workloads so you have tooling and emulators
1. .NET 6 Preview Runtime and SDK

* Windows: [dotnet-sdk-6.0.100-preview.2.21155.3-win-x64.exe](https://dotnetcli.azureedge.net/dotnet/Sdk/6.0.100-preview.2.21155.3/dotnet-sdk-6.0.100-preview.2.21155.3-win-x64.exe)
* macOS: [dotnet-sdk-6.0.100-preview.2.21155.3-osx-x64.pkg](https://dotnetcli.azureedge.net/dotnet/Sdk/6.0.100-preview.2.21155.3/dotnet-sdk-6.0.100-preview.2.21155.3-osx-x64.pkg)

3. Platform SDKs compatible with .NET 6 Preview 2

Android:

* Windows: [Microsoft.NET.Workload.Android.11.0.200.148.msi](https://dl.internalx.com/vsts-devdiv/Xamarin.Android/public/net6/4534967/main/f4d8fe238b15eadfc7842749bf13e5fca3e2f2d2/Microsoft.NET.Workload.Android.11.0.200.148.msi)
* macOS: [Microsoft.NET.Workload.Android-11.0.200.148.pkg](https://dl.internalx.com/vsts-devdiv/Xamarin.Android/public/net6/4534967/main/f4d8fe238b15eadfc7842749bf13e5fca3e2f2d2/Microsoft.NET.Workload.Android-11.0.200-ci.f4d8fe238b15eadfc7842749bf13e5fca3e2f2d2.148.pkg)

iOS:

* Windows: [Microsoft.NET.Workload.iOS.14.4.100-ci.main.1192.msi](https://bosstoragemirror.azureedge.net/wrench/main/98c8649d0c7d1e3c4c8d8d09e022befa853fb1e7/4541181/package/Microsoft.NET.Workload.iOS.14.4.100-ci.main.1192.msi)
* macOS: [Microsoft.iOS.Bundle.14.4.100-ci.main.1192.pkg](https://bosstoragemirror.azureedge.net/wrench/main/98c8649d0c7d1e3c4c8d8d09e022befa853fb1e7/4541181/package/notarized/Microsoft.iOS.Bundle.14.4.100-ci.main.1192.pkg)

Mac Catalyst:

* macOS: [Microsoft.MacCatalyst.Bundle.14.3.100-ci.main.337.pkg](https://bosstoragemirror.azureedge.net/wrench/main/98c8649d0c7d1e3c4c8d8d09e022befa853fb1e7/4541181/package/notarized/Microsoft.MacCatalyst.Bundle.14.3.100-ci.main.337.pkg)


_NOTE: newer builds of .NET *may* work, but your mileage may vary.
The workload installers enable a feature flag file via
`sdk/6.0.100-preview.2.21155.3/EnableWorkloadResolver.sentinel`, which would
need to be created manually for other .NET 6 versions. You can find
the full list of builds at the [dotnet/installer][dotnet/installer]
repo._

## To Make Your Exploration More Enjoyable

1. Install the .NET MAUI Project Templates

Open a terminal and run:

```
dotnet new --install Microsoft.Maui.Templates::6.0.100-preview.2.2.159 --nuget-source https://pkgs.dev.azure.com/azure-public/vside/_packaging/xamarin-impl/nuget/v3/index.json
```

> Note: you can bump the version or try a * wildcard on Windows as templates will continue to be updated.

## Time to Go!

1. Start a New Project

```
dotnet new maui-mobile -n FirstLook
```

2. Open the project in Visual Studio Code.

At this time it's easiest to edit in your favorite editor, and build from the command line.

```
code ./FirstLook
```

3. Restore the NuGets 

Add a `nuget.config` file to the root of your project with the following:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <packageSources>
    <clear />
    <!-- ensure only the sources defined below are used -->
    <add key="dotnet6" value="https://pkgs.dev.azure.com/dnceng/public/_packaging/dotnet6/nuget/v3/index.json" />
    <add key="xamarin" value="https://pkgs.dev.azure.com/azure-public/vside/_packaging/xamarin-impl/nuget/v3/index.json" />
  </packageSources>
</configuration>
```

VS Code will often prompt you to restore, however you can restore a few other ways.

With VS Code commands:

> Type `SHFT+CMD+P` and type restore to choose the restore command.

With dotnet cli:

```
dotnet restore
```

NOTE: you may need to run this targeting both projects, the library and the iOS, by running it within the iOS folder as well. Alternatively use `msbuild /t:restore`. 

4. Surf the .NET 6 Wave!

In Visual Studio for Windows, select your device or emulator from the selector and click the play button (or hit F5).

With dotnet cli from within your project directory:

```
dotnet build -t:Run -f net6.0-android
dotnet build -t:Run -f net6.0-ios
dotnet build -t:Run -f net6.0-maccatalyst
```

> NOTE: You may need to add the `--no-restore` switch until
> [dotnet#15485](https://github.com/dotnet/sdk/issues/15485) is
> resolved.

## Using IDEs

Currently, you can use Visual Studio 2019 16.9 on Windows (with the
Xamarin workload) with a few manual steps.

Open an Administrator command prompt to enable the
`EnableWorkloadResolver.sentinel` feature flag:

    > cd "%ProgramFiles(x86)%\Microsoft Visual Studio\2019\Enterprise\MSBuild\Current\Bin\SdkResolvers\Microsoft.DotNet.MSBuildSdkResolver"
    > echo > EnableWorkloadResolver.sentinel

Or in an Administrator `powershell` prompt:

    > cd "${env:ProgramFiles(x86)}\Microsoft Visual Studio\2019\Enterprise\MSBuild\Current\Bin\SdkResolvers\Microsoft.DotNet.MSBuildSdkResolver"
    > '' > EnableWorkloadResolver.sentinel

> NOTE: your path to Visual Studio may vary, depending on where you
> selected to install it. `Enterprise`, `Professional`, or `Community`
> might be correct depending on the SKU you have installed.

This command creates an empty file that enables .NET workload support.
Restart Visual Studio after making this change.

Visual Studio for Mac support will be coming in a future release.

### iOS from Visual Studio

To build and debug .NET 6 iOS applications from Visual Studio 2019 you
must manually intall the .NET 6 SDK and iOS workloads on both
**Windows and macOS** (Mac build host).

If while connecting Visual Studio to your Mac through XMA you are
prompted to install a different version of the SDK, you can ignore
that since it refers to the legacy one.

> Note: currently only the iOS simulator is supported.

### Mac Catalyst from Visual Studio for Mac

Running and debugging apps from Visual Studio for Mac does not work yet.

### Known Issues

* There are no project property pages available for both iOS and
  Android
* Editors (i.e. Manifest editor, Entitlements editor, etc.) will fail
  to open, so as a workaround please open those files with the XML
  editor.