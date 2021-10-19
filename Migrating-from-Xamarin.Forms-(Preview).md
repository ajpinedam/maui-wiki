To bring your Xamarin.Forms projects to .NET 6 and update the code to .NET MAUI, you will (generally) need to do a few things:

* Convert the projects from .NET Framework to .NET SDK Style
* Update code namespaces
* Update any incompatible NuGet packages
* Address any breaking API changes

At this time the .NET Upgrade Assistant will do the first few steps for you. Be aware, this tool is incomplete. Please [file feedback](https://github.com/dotnet/upgrade-assistant/issues) so we can improve the tool for everyone!

## Get Started

> Use source control! The assistant will try to make a backup for you, but please take care.

Install the .NET Upgrade Assistant dotnet tool: 

```
dotnet tool install --global upgrade-assistant --version 0.2.241603
```

Start the upgrade process and follow the interactive instructions:

```
upgrade-assistant upgrade <Path to csproj or sln to upgrade>
```

### Limitations
-	Must be on Xamarin.Forms 4.8 or higher
-	Only works with Xamarin.Forms .slns (Xamarin.Android and Xamarin.iOS only solutions coming later)
-	Will not work with binding or library projects
-	Gets you _most_ of the way there – you’ll still have to do some manual changes too

### Features coming soon

1. Nuget Package analysis
2. XAML source code updates

### Known issues

1. Repeated logs/messages
2. UWP project check might be weird sometimes => being worked on
3. It adds an extra UA analyzer package to project => being worked on
