## Remove "Assets" from Windows image paths

* [Improve consistency with resizetizer](https://github.com/dotnet/maui/pull/4367)

Update paths in "Platform/Windows/Package.appxmanifest" to remove "Assets" from file paths.

If you have anywhere stated the location of images for Windows, you'll want to remove that. For example:

```xaml
<Application xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:windows="clr-namespace:Microsoft.Maui.Controls.PlatformConfiguration.WindowsSpecific;assembly=Microsoft.Maui.Controls"
             windows:Application.ImageDirectory="Assets"
             x:Class="WeatherTwentyOne.App">
```

should now be

```xaml
<Application xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="WeatherTwentyOne.App">
```

## Control Changes

* `GridLayout` name has been removed in favor of the original `Grid` naming to remedy confusion

## Raw Assets
This is new addition to the templates, but you will fine a new folder under `Resources` named `Raw`, with a file named `AboutAssets.txt`. This file type is set to `MauiAsset` as the Build Action. Inside of it you will find:

```
Any raw assets you want to be deployed with your application can be placed in
this directory (and child directories) and given a Build Action of "MauiAsset":

	<MauiAsset Include="AboutAssets.txt" />

These files will be deployed with you package and will be accessible using Essentials:

	async Task LoadMauiAsset()
	{
		using var stream = await FileSystem.OpenAppPackageFileAsync("AboutAssets.txt");
		using var reader = new StreamReader(stream);

		var contents = reader.ReadToEnd();
	}
```

Inside of your `.csproj` you can include all Raw assets by adding the following property under the `MauiFont` configuration:

```xml
    <MauiAsset Include="Resources\Raw\**" LogicalName="%(RecursiveDir)%(Filename)%(Extension)" />
```


## .NET MAUI Essentials
.NET MAUI Essentials is now automatically configured when you initiatlize .NET MAUI in your `MauiProgram.cs`. You can remove the following boilerplate code from the the individual platforms:

### Android

In the `MainActivity.cs` you can remove all code inside of the class so it looks like:

```csharp
[Activity(Theme = "@style/Maui.SplashTheme", MainLauncher = true, ConfigurationChanges = ConfigChanges.ScreenSize | ConfigChanges.Orientation | ConfigChanges.UiMode | ConfigChanges.ScreenLayout | ConfigChanges.SmallestScreenSize)]
public class MainActivity : MauiAppCompatActivity
{
}
```

### Windows

In your `App.xaml.cs` inside of the Windows folder you can remove `OnLaunched` and it should now look like:

```csharp
public partial class App : MauiWinUIApplication
{
    /// <summary>
    /// Initializes the singleton application object.  This is the first line of authored code
    /// executed, and as such is the logical equivalent of main() or WinMain().
    /// </summary>
    public App()
    {
        this.InitializeComponent();
    }

    protected override MauiApp CreateMauiApp() => MauiProgram.CreateMauiApp();
}
```

