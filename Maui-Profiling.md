## Setup

Until this PR (https://github.com/dotnet/maui/issues/822) is merged, we will have to use the Android SDK files from that. There is a "nuget-unsigend" artifact. Put the nupkg files into a place:

 - add it to the nuget.config: https://github.com/dotnet/maui/blob/main/src/DotNet/DotNet.csproj#L80
 - update the versions: https://github.com/dotnet/maui/blob/main/eng/Versions.props
 - run dotnet build on the DotNet.csproj


## App

Create a new app (or something) and then add this to a Directory.Build.props:

```xml
<Project>
    <PropertyGroup Condition=" '$(Enable64BitBuild)' != 'True' ">
        <RuntimeIdentifiers>android-arm;android-x86</RuntimeIdentifiers>
    </PropertyGroup>
    <PropertyGroup Condition=" '$(Enable64BitBuild)' == 'True' ">
        <RuntimeIdentifiers>android-arm64;android-x64</RuntimeIdentifiers>
    </PropertyGroup>
</Project>
```

Make sure the `<UseInterpreter>` is OFF.

For emulator builds, add this to the Android environment variables (port 9000 is random):

```
DOTNET_DiagnosticPorts=10.0.2.2:9000,suspend
```

> There is more instructions here for devices: https://gist.github.com/grendello/0e0829dd159bac26d9a5558735a99a2e

## Tools

You will need this repo for the `dotnet-dsrouter` tool: https://github.com/dotnet/diagnostics

Run the router tool (I just did dotnet run, note the 9000 port number):

```
dotnet run --project C:\Projects\diagnostics\src\Tools\dotnet-dsrouter\dotnet-dsrouter.csproj -- client-server -tcps 127.0.0.1:9000 -ipcc /tmp/maui-app --verbose debug
```

Install and run the `dotnet-trace` tool from nuget:

```
dotnet-trace collect --diagnostic-port /tmp/maui-app --format speedscope -o C:/tmp/hellomaui-app-trace
```

Then the app launches, this tool will start receiving data. Once the data is collected enough, hit Enter and it will terminate the tool and output the trace to "C:/tmp/hellomaui-app-trace". Open thejson file in https://www.speedscope.app/

Use the local dotnet build to run the app (seems profiling only works in 64-bit):

```
..\..\bin\dotnet\dotnet.exe build -f net6.0-android -t:run -c Release -p:AndroidLinkResources=true -p:AndroidEnableProfiler=true -p:Enable64BitBuild=true
```


> I have a hacky branch for my system for now: https://github.com/dotnet/maui/compare/dev/testing-profiling-hacks