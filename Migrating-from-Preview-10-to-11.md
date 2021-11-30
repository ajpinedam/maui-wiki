## .csproj

Windows App SDK is now version 1.0.0

```xml
<ItemGroup Condition="$(TargetFramework.Contains('-windows'))">
	<PackageReference Include="Microsoft.WindowsAppSDK" Version="1.0.0" />
	<PackageReference Include="Microsoft.Graphics.Win2D" Version="1.0.0.30" />
</ItemGroup>
```