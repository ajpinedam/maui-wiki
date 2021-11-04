### Windows changes

Windows is now supported by default. Update the Windows references:

```xml
<PropertyGroup>
	<TargetFrameworks>net6.0-android;net6.0-ios;net6.0-maccatalyst</TargetFrameworks>
	<TargetFrameworks Condition="$([MSBuild]::IsOSPlatform('windows')) and '$(MSBuildRuntimeType)' == 'Full'">$(TargetFrameworks);net6.0-windows10.0.19041</TargetFrameworks>
	...
</PropertyGroup>
```

Replace your Windows package references with the these two:

```xml
<ItemGroup Condition="$(TargetFramework.Contains('-windows'))">
	<!-- Required - WinUI does not yet have buildTransitive for everything -->
	<PackageReference Include="Microsoft.WindowsAppSDK" Version="1.0.0-preview3" />
	<PackageReference Include="Microsoft.Graphics.Win2D" Version="1.0.0.29-preview3" />
</ItemGroup>
```

Update `SupportedOSPlatformVersion` and add new `TargetPlatformMinVersion` in the first `<PropertyGroup>`.

```xml
<SupportedOSPlatformVersion Condition="$(TargetFramework.Contains('-windows'))">10.0.17763.0</SupportedOSPlatformVersion>
<TargetPlatformMinVersion Condition="$(TargetFramework.Contains('-windows'))">10.0.17763.0</TargetPlatformMinVersion>
```

Update the RuntimeIdentifier:

```xml
<PropertyGroup Condition="$(TargetFramework.Contains('-windows'))">
	<OutputType>WinExe</OutputType>
	<RuntimeIdentifier>win10-x64</RuntimeIdentifier>
</PropertyGroup>
```

### New MauiIcon

For the app icon, update your `<MauiImage IsAppIcon="True">` to use the new type `<MauiIcon />`.

```xml
<MauiIcon Include="Resources\appicon.svg" ForegroundFile="Resources\appiconfg.svg" Color="#512BD4" />
```

## Optional Updates

Our new templates have now adopted .NET 6-isms such as [global using](https://github.com/dotnet/maui/blob/main/src/Templates/src/templates/maui-mobile/GlobalUsings.cs) and [scoped namespaces](https://github.com/dotnet/maui/commit/e9eb388f61825d75b361b81bf2798b863503254e). 