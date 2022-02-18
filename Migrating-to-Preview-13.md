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

