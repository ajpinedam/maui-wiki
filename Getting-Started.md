## Installing with .NET MAUI Check Tool

This is a community-supported, open-source, global dotnet tool that will evaluate your development environment and guide you to install and configure everything you need to build a .NET MAUI application.

Install: `dotnet tool install -g redth.net.maui.check`

Run: `maui-check`

This will check for:
 - OpenJdk / AndroidSDK
 - .NET 6 Preview SDK
 - .NET MAUI / iOS / Android workloads and packs
 - .NET MAUI Templates
 - Workload Resolver .sentinel files for dotnet and Visual Studio Windows/Mac
 - Currently does not install workloads required for WinUI3

For more information and source code, visit [redth/dotnet-maui-check](https://github.com/redth/dotnet-maui-check).

To manually install your environment, follow the [instructions here](https://github.com/dotnet/net6-mobile-samples/tree/develop#installing-with-official-preview-installers). 

To use WinUI 3, follow the instructions to get started with [Project Reunion](https://docs.microsoft.com/en-us/windows/apps/project-reunion/get-started-with-project-reunion#set-up-your-development-environment).

## Time to Go!

1. Start a New Project

```
dotnet new maui -n HelloMauiPreview
```

2. Open the project in Visual Studio Code.

At this time it's easiest to edit in your favorite editor, and build from the command line.

```
code ./HelloMauiPreview
```

3. Restore the NuGets 

Create a `nuget.config` file to the root of your project and add the following feed(s) with these commands:

```
dotnet new nugetconfig
dotnet nuget add source -n maui-preview https://aka.ms/maui-preview/index.json
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

> WinUI 3 requires you to build and deploy with the latest preview of Visual Studio 2019 16.10.

## Using IDEs

Currently, we recommend using the latest preview version of Visual Studio 2019 16.10 on Windows (with the
Xamarin workload). If you used `maui-check` then you're configured! 

Otherwise, follow these additional steps:

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
must manually install the .NET 6 SDK and iOS workloads on both
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