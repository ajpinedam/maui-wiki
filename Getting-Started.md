## Pre-requisites

Follow the [installation instructions here](https://docs.microsoft.com/en-us/dotnet/maui/get-started/installation).

## Create your first .NET MAUI app

1. Start a New Project

```console
$ dotnet new maui -n HelloMauiPreview
```

2. Open the project in Visual Studio 2022 on Windows, or Visual Studio Code on macOS.

```console
$ code ./HelloMauiPreview
```

3. Restore the NuGets. Visual Studio will do this for you by default. You can also restore via CLI with:

```console 
$ dotnet restore
```

4. Surf the .NET 6 Wave!

In Visual Studio for Windows, select your device or emulator from the selector and click the play button (or hit F5).

![Visual Studio run menu](https://devblogs.microsoft.com/dotnet/wp-content/uploads/sites/10/2021/05/run-static-profiles.png)

Optionally, you can build and run your .NET MAUI application from CLI using one of the following commands:

```console
$ dotnet build -t:Run -f net6.0-android
$ dotnet build -t:Run -f net6.0-ios -p:_DeviceName=:v2:udid=<UDID>
$ dotnet build -t:Run -f net6.0-maccatalyst
```

These commands will launch the application on the default device, if one can be found. For Android, it's best to have an emulator up and running first. To find an iOS device UDID, [follow these directions](https://github.com/dotnet/maui/wiki/CLI:-iOS-Simulator-Selection).