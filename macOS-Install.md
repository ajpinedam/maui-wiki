### Pre-requisites

* Xcode 13 [latest version](https://xcodereleases.com/) - available in the Mac App Store and from [https://developer.apple.com](https://developer.apple.com)
* [Android Studio](https://developer.android.com/studio) 
  * Latest Android SDK (API 31 or newer)
  * Android Emulator (optional) - once installed, create and start an Android emulator. Optionally, you can use an Android device configured for development.
* [OpenJDK 11](https://docs.microsoft.com/en-us/java/openjdk/download#openjdk-11)
* [VS Code](https://code.visualstudio.com/) (recommended) 
  * [Omnisharp extension](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp)

## Install .NET 6 with .NET MAUI

1. Download and run the latest .NET 6 installer from [dotnet/installer](https://github.com/dotnet/installer/blob/main/README.md#installers-and-binaries). 
2. Open Terminal and check that you're ready to install .NET MAUI.

```
> dotnet --version
```

**Option A)** Install .NET MAUI using workload install command:

```
> sudo dotnet workload install maui --source https://api.nuget.org/v3/index.json
```

> Why use `--source`? The CLI will use any "nuget.config" found up your directory structure. By explicitly providing the public source, you ensure the latest public builds will be found.

This command will get you the latest released version of .NET MAUI plus the platform SDKs for Android, iOS, macOS, and Windows. 

**Option B)** Pass in additional parameters to the same command in order to get a **specific branch build**. 

```
> sudo dotnet workload install maui --from-rollback-file https://aka.ms/dotnet/maui/preview.14.json --source https://aka.ms/dotnet6/nuget/index.json --source https://api.nuget.org/v3/index.json
```

Your app will use the newest version available on your system. 

> These commands can be found in the contributor's [development guide on dotnet/maui](https://github.com/dotnet/maui/blob/main/.github/DEVELOPMENT.md)

That's it! You now have the building blocks to create, build, and run a .NET MAUI app. Let's do that.

## New App

To create a new app run:

```
> dotnet new maui -n "MyMauiApp"
```

CD into the "MyMauiApp" directory and run the app:

```
> dotnet build -t:Run -f net6.0-maccatalyst
```

![Xcode Devices and Simulators](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/7mi23lod2z06m0j85di1.png)

This will restore the project dependencies, compile the app, and launch it. The ``-f`` parameter is the "target framework moniker". Options include:

* net6.0-android
* net6.0-ios
* net6.0-maccatalyst

> To run Windows on Windows you need Visual Studio 2022. 

### Targeting iOS

In order to target an iOS emulator, you need to provide the device id (UUID). Open Xcode and then go to Windows > Devices and Simulators. Right-click the simulator you want to use and copy the "Device Identifier".

![app running on macOS](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/vezefpi5aev3oziqk2ef.png)

Now append the value to the parameter ``-p:_DeviceName=:v2:uuid=``:

```
> dotnet build -t:Run -f net6.0-ios -p:_DeviceName=:v2:udid=02C556DA-64B8-440B-8F06-F8C56BB7CC22
```

### Targeting Android

Before building the Android app, start an emulator or connect to a device using ``adb connect``. Then you can run:

```
> dotnet build -t:Run -f net6.0-android
```

![app running on Android](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/k98ye6rqfejcvxz2s7r1.png)

> **Troubleshooting tip:** if you get an error indicating you need to set the JavaSdkDirectory in Visual Studio, you may need to  add the following to a file "Directory.Build.props" in your project directory.

```
<Project>
    <PropertyGroup>
        <JavaSdkDirectory Condition="'$(JavaSdkDirectory)'=='' and '$(JAVA_HOME_8_X64)'!=''">$(JAVA_HOME_8_X64)</JavaSdkDirectory>
    </PropertyGroup>
</Project>
```