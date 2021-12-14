## .csproj

Windows App SDK is now version 1.0.0

```xml
<ItemGroup Condition="$(TargetFramework.Contains('-windows'))">
	<PackageReference Include="Microsoft.WindowsAppSDK" Version="1.0.0" />
	<PackageReference Include="Microsoft.Graphics.Win2D" Version="1.0.0.30" />
</ItemGroup>
```

## Multi-window iOS, iPadOS, and Mac Catalyst

Add to Platforms/*/info.plist:

```xml
<key>UIApplicationSceneManifest</key>
<dict>
	<key>UIApplicationSupportsMultipleScenes</key>
	<true/>
	<key>UISceneConfigurations</key>
	<dict>
		<key>UIWindowSceneSessionRoleApplication</key>
		<array>
			<dict>
				<key>UISceneConfigurationName</key>
				<string>__MAUI_DEFAULT_SCENE_CONFIGURATION__</string>
				<key>UISceneDelegateClassName</key>
				<string>SceneDelegate</string>
			</dict>
		</array>
	</dict>
</dict>
```

In each platform, add a [SceneDelegate.cs](https://github.com/dotnet/maui/blob/main/src/Controls/samples/Controls.Sample.SingleProject/Platforms/MacCatalyst/SceneDelegate.cs). For example:

```csharp
using Foundation;
using Microsoft.Maui;
using ObjCRuntime;
using UIKit;

namespace Maui.Controls.Sample;

[Register("SceneDelegate")]
public class SceneDelegate : MauiUISceneDelegate
{

}
```

