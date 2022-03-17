## Xamarin.Forms vs .NET MAUI


|  |Xamarin.Forms  |.NET MAUI  |
|---------|---------|---------|
|**Platforms**     |         |         |
|Android     |API 19+        |API 21+        |
|iOS     |9-15         |10+         |
|Linux     |Community         |[Community](https://github.com/jsuarezruiz/maui-linux)         |
|macOS     |Community         |Microsoft         |
|Tizen     |Samsung           |[Samsung](https://github.com/Samsung/Tizen.NET)           |
|Windows     |UWP Microsoft<br/>WPF Community         |Microsoft<sup>*</sup>         |
|**Features**     |         |         |
|Renderers     |Tightly coupled to BindableObject         |Loosely coupled, no Xamarin.Forms dependencies         |
|App Models     |MVVM         |MVVM         |
|     |RxUI         |RxUI         |
|     |             |MVU <sup>**</sup> |
|     |             |Blazor <sup>**</sup> |
|Single Project     |No         |Yes         |
|Multi-targeting     |No         |Yes         |
|Multi-window     |No         |Yes         |
|**Misc**     |         |         |
|.NET     |Xamarin.iOS, Xamarin.Android, Mono, .NET Framework, ...         |.NET 6+         |
|XAML Hot Reload|Experimental: SDK 4.x & Visual Studio 2019 prior to version 16.9<br>Feature Complete: SDK 5.x & Visual Studio 2019 version 16.9 or newer|Yes|
|.NET Hot Reload|iOS/Android – No<br>UWP – Limited support for runtime edits using .NET “Edit & Continue”|Yes|
|Acquisition |NuGet & Visual Studio Installer |dotnet |
|Project System     |Franken-proj         |SDK Style         |
|dotnet CLI     |No         |Yes         |
|**Tools**     |         |         |
|Visual Studio 2022     |Yes         |Yes         |
|Visual Studio 2022 for Mac     |Yes         |Yes         |
|Visual Studio Code     |No         |Experimental<sup>***</sup>         |

<sup>*</sup> The Windows implementation is Windows App SDK with WinUI 3.

<sup>**</sup> These app models are experimental.

<sup>***</sup> Visual Studio Code will work by virtue of .NET unification, however not all experiences that make .NET MAUI development delightful (intellisense for example) may be enabled at the time of .NET 6 release.