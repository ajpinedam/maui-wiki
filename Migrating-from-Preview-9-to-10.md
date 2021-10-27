## csproj

Update the Windows references:

```xml
<ItemGroup Condition="$(TargetFramework.Contains('-windows'))">
		<!-- Required - WinUI does not yet have buildTransitive for everything -->
		<PackageReference Include="Microsoft.WindowsAppSDK" Version="1.0.0-preview2" />
		<PackageReference Include="Microsoft.Graphics.Win2D" Version="1.0.0.28-preview2" />
	</ItemGroup>
```

Update `SupportedOSPlatformVersion` and add new `TargetPlatformMinVersion` in the first `<PropertyGroup>`.

```xml
<SupportedOSPlatformVersion Condition="$(TargetFramework.Contains('-windows'))">10.0.17763.0</SupportedOSPlatformVersion>
		<TargetPlatformMinVersion Condition="$(TargetFramework.Contains('-windows'))">10.0.17763.0</TargetPlatformMinVersion>
```