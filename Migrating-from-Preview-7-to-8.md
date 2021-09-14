This document covers the main differences between previews that you'll need to adopt as you are updating projects from release to release. 

### Pre-Steps

* Uninstall all versions of .NET 6 previews via Add/Remove Programs
* Uninstall all versions of Visual Studio 2022

### Minimum Requirements

* Visual Studio 2022 Preview 4 with .NET MAUI workload requirements (see [installation docs](https://docs.microsoft.com/dotnet/maui))
* Android API 31 obtained via Android Studio
* [OpenJDK 11](https://www.microsoft.com/openjdk)
* Xcode 13 latest beta (Mac build host)
* [Single Project extension](https://marketplace.visualstudio.com/items?itemName=ProjectReunion.MicrosoftSingleProjectMSIXPackagingToolsDev17) for Windows App SDK

## 1 - Startup.cs to MauiProgram.cs

.NET MAUI now aligns with ASP.NET and Blazor with our usage of this host builder pattern. 

1. Rename Startup.cs to MauiProgram.cs
2. Update the class and method to match [the template](https://github.com/dotnet/maui/blob/main/src/Templates/src/templates/maui-mobile/MauiProgram.cs#L8-L22)

```csharp
using Microsoft.Maui;
using Microsoft.Maui.Hosting;
using Microsoft.Maui.Controls.Compatibility;
using Microsoft.Maui.Controls.Hosting;

namespace MauiApp._1
{
	public static class MauiProgram
	{
		public static MauiApp CreateMauiApp()
		{
			var builder = MauiApp.CreateBuilder();
			builder
				.UseMauiApp<App>()
				.ConfigureFonts(fonts =>
				{
					fonts.AddFont("OpenSans-Regular.ttf", "OpenSansRegular");
				});

			return builder.Build();
		}
	}
}
```

3. Update `Platforms/Android/MainApplication.cs` to implement `CreateMauiApp()` and update the class inheritance. Do the same for `Platforms/iOS/AppDelegate.cs`, and `Platforms/MacCatalyst/AppDelegate.cs`.

```csharp
using System;
using Android.App;
using Android.Runtime;
using Microsoft.Maui;

namespace MauiApp._1
{
	[Application]
	public class MainApplication : MauiApplication
	{
		public MainApplication(IntPtr handle, JniHandleOwnership ownership)
			: base(handle, ownership)
		{
		}

		protected override MauiApp CreateMauiApp() => MauiProgram.CreateMauiApp();
	}
}
```

## 2 - Windows Platform Single Project

The Windows platform is now part of the .NET MAUI single project. 

1. Use the template to add the base files to `Platforms/Windows` and update for your namespace.
2. Copy into `Platforms/Windows` and platform specific code you have in your Windows project.
3. Add any NuGet dependencies specific to Windows to the Single Project.
4. Add [launchSettings.json](https://github.com/dotnet/maui/blob/main/src/Templates/src/templates/maui-mobile/Properties/launchSettings.json) to the Properties folder.
5. Remove your Windows project from the solution.
6. Update your csproj file with the Windows TargetFramework and platform dependencies.

```xml

<Project Sdk="Microsoft.NET.Sdk">

	<PropertyGroup>
		<TargetFrameworks>net6.0-ios;net6.0-android;net6.0-maccatalyst</TargetFrameworks>
		<!-- <TargetFrameworks Condition="$([MSBuild]::IsOSPlatform('windows')) and '$(MSBuildRuntimeType)' == 'Full'">$(TargetFrameworks);net6.0-windows10.0.19041</TargetFrameworks> -->
		<OutputType>Exe</OutputType>
		<RootNamespace>MauiApp._1</RootNamespace>
		<UseMaui>true</UseMaui>
		<SingleProject>true</SingleProject>
		<EnablePreviewMsixTooling>true</EnablePreviewMsixTooling>

		<!-- Display name -->
		<ApplicationTitle>MauiApp.1</ApplicationTitle>

		<!-- App Identifier -->
		<ApplicationId>com.companyname.MauiApp._1</ApplicationId>

		<!-- Versions -->
		<ApplicationVersion>1.0</ApplicationVersion>
		<AndroidVersionCode>1</AndroidVersionCode>

		<!-- Required for C# Hot Reload -->
		<UseInterpreter Condition="'$(Configuration)' == 'Debug'">True</UseInterpreter>
	</PropertyGroup>

	<ItemGroup>
		<!-- App Icon -->
		<MauiImage
			Include="Resources\appicon.svg"
			ForegroundFile="Resources\appiconfg.svg"
			IsAppIcon="true"
			Color="#512BD4" />

		<!-- Splash Screen -->
		<MauiSplashScreen Include="Resources\appiconfg.svg" Color="#512BD4" />

		<!-- Images -->
		<MauiImage Include="Resources\Images\*" />

		<!-- Custom Fonts -->
		<MauiFont Include="Resources\Fonts\*" />
	</ItemGroup>

	<ItemGroup Condition="$(TargetFramework.Contains('-windows'))">
		<!-- Required - WinUI does not yet have buildTransitive for everything -->
		<PackageReference Include="Microsoft.WindowsAppSDK" Version="WINDOWSAPPSDK_VERSION" />
		<PackageReference Include="Microsoft.WindowsAppSDK.Foundation" Version="WINDOWSAPPSDK_VERSION" />
		<PackageReference Include="Microsoft.WindowsAppSDK.WinUI" Version="WINDOWSAPPSDK_VERSION" />
		<PackageReference Include="Microsoft.WindowsAppSDK.InteractiveExperiences" Version="WINDOWSAPPSDK_VERSION" NoWarn="NU1701" />
	</ItemGroup>

	<PropertyGroup Condition="$(TargetFramework.Contains('-windows'))">
		<OutputType>WinExe</OutputType>
		<RuntimeIdentifier>win-x64</RuntimeIdentifier>
	</PropertyGroup>
	
	<PropertyGroup>
		<!-- Required - WinUI can't deploy in a multi-targeting environment -->
		<RuntimeIdentifier Condition="$(TargetFramework.Contains('-windows'))">win-x64</RuntimeIdentifier>
	</PropertyGroup>

</Project>
```

## 3 - Update Android Theme

Android now uses the MaterialTheme which may conflict with older themes and styles. Update your `MainActivity.cs` and/or styles.xml to be based on the `@style/Maui.SplashTheme` Theme.

```csharp
using Android.App;
using Android.Content.PM;
using Microsoft.Maui;

namespace MauiApp._1
{
	[Activity(Theme = "@style/Maui.SplashTheme", MainLauncher = true, ConfigurationChanges = ConfigChanges.ScreenSize | ConfigChanges.Orientation | ConfigChanges.UiMode | ConfigChanges.ScreenLayout | ConfigChanges.SmallestScreenSize)]
	public class MainActivity : MauiAppCompatActivity
	{
	}
}
```