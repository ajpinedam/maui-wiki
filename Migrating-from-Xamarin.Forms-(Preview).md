To bring your Xamarin.Forms projects to .NET 6 and update the code to .NET MAUI, you will (generally) need to do a few things:

* Convert the projects from .NET Framework to .NET SDK Style
* Update code namespaces
* Update any incompatible NuGet packages
* Address any breaking API changes

# Manual Migration Steps 

Please note these steps might change as we get closer to GA, but generally the process would remain the same. Currently we would recommend following these manual steps as we continue work on the .NET upgrade-assistant tool to provide a quicker upgrade process. 

These steps are for Xamarin.Forms apps using Xamarin.Forms version 5.0 or higher, for best experience. 

> ⌚ Please refresh/come back to this page as we update it with more findings/steps. 🔥

## Supported Project types and minimum requirements

- Xamarin.Forms app using Xamarin.Forms 5.0 or higher
  - ✅ iOS project
  - ✅ Android project
  - ❌ UWP project 
  - ❌ iOS App extension and other extension types for example Share Extension project

- Complete environment setup for .NET MAUI including all necessary workloads installed. Confirm that your environment can build and run a blank .NET MAUI template app. Be sure to follow all steps mentioned in the [Getting Started](https://github.com/dotnet/maui/wiki#getting-started). 

## Getting Started

Before you start the migration process, make note of the following:

- Use source control and create a branch to work on the migrated project. If you do not use source control, please create a backup of your project before starting any migration related work. You will refer back to your original project so it's important to keep a copy available. 

- For the global updates like namespaces etc, using [VSCode](https://code.visualstudio.com/Download) is recommended, makes life easy. 

- Migration on Windows using [Visual Studio 2022 Previews](https://visualstudio.microsoft.com/vs/preview/) is the best path at the moment. You can easily build the project and find namespaces or alias code or references that need fixing a lot quicker. Provided you have all the .NET MAUI workloads installed, you can migrate both your Android and iOS projects on Windows itself and confirm the code compiles. After that you can test the app running on the respective platforms, on your Mac and Windows machine as needed.

- Migration on Mac, using [Visual Studio 2022 for Mac Preview 8](https://devblogs.microsoft.com/visualstudio/visual-studio-2022-for-mac-preview-8/) or newer Previews. After making the initial project file updates, you can open the `sln` in the IDE, build the project to find errors and fix them easily. After that you can test the app running on their respective platforms. 

> If you are on Mac only environment and don't want to install Visual Studio for Mac Previews, please follow the [Mac Install Guide Pre-requisites](https://visualstudio.microsoft.com/vs/preview/) to ensure you have all the necessary tooling. You can then run the CLI commands for building and running. 

- Be sure to Clean and Build after every change you make, even better, delete the bin/obj folders manually to make sure you are always testing the most recent changes. 

## Tips/Tricks and Handy Links 

- [.NET MAUI Documentation](https://docs.microsoft.com/en-us/dotnet/maui/) is being updated almost everyday with documentation about controls, layouts, gestures (pretty much everything!!!) and is the perfect place to check for new APIs or how to register custom controls or create a new custom controls via handlers.
- .NET6.0 iOS Migration : [Project File Properties](https://github.com/xamarin/xamarin-macios/wiki/Project-file-properties-dotnet-migration)
- .NET6.0 Android Migration : [Project File Properties](https://github.com/xamarin/xamarin-android/blob/main/Documentation/guides/OneDotNet.md)
- To build and run the migrated projects via `dotnet cli` use the following commands : ( `-t:Run` will run the app, so to only build, remove that from the command)
  - iOS : `dotnet build <path_to_iOS_csproj_file> -f net6.0-ios -c Debug -t:Run`
  - Android: `dotnet build <path_to_Android_csproj_file> -f net6.0-ios -c Debug -t:Run`
- If you are hitting build issues in VS2022 or the app builds but does not deploy, check the Configuration Mapping for your solution and select the appropriate options.
- Expect a lot of namespace clashes or expect to add a lot of alias and fully qualified paths instead of just `using` statements.

## Samples
Stay tuned for more migrated samples to be added here :
- Use branch `maui-projecthead` for ArtAuction App (non-Shell) : https://github.com/Sweekriti91/ArtAuction/tree/maui-projecthead
- Use branch `maui-migrate` for PlantLady App (uses Shell) : https://github.com/maddymontaquila/PlantLady/tree/maui-migrate
- 😎 a few more complex project samples coming soon! 👀 this space

Library and Custom Control migration samples in Javier's repo [here](https://github.com/jsuarezruiz/mvpsummit2022-dotnet-maui).

## Migration Steps

### Step 1 : csproj files updates
- [**Xamarin.Forms Project** -> _now_ **.NET MAUI Project**] Make the following updates to your `csproj` by referring to one of the migrated samples to get an overall view of all changes necessary. 
  - Follow Sample [csproj here](https://github.com/maddymontaquila/PlantLady/blob/maui-migrate/PlantLady/PlantLady/PlantLady.csproj)
  - Important new Project properties:
    ``` 
    <TargetFrameworks>net6.0-ios;net6.0-android</TargetFrameworks>
    <UseMaui>True</UseMaui>
    <OutputType>Library</OutputType>
    ```
- [**Xamarin.iOS Project** -> _now_ **.NET MAUI iOS Project**] and  [**Xamarin.Android Project** -> _now_ **.NET MAUI Android Project**] Make the following updates to your `csproj` by referring to one of the migrated samples to get an overall view of all changes necessary. 
  - Follow Sample [iOS csproj here](https://github.com/Sweekriti91/ArtAuction/blob/maui-projecthead/ArtAuction.iOS/ArtAuction.iOS.csproj) and [Android csproj here](https://github.com/Sweekriti91/ArtAuction/blob/maui-projecthead/ArtAuction.Android/ArtAuction.Android.csproj).
  - Important new Project properties:
    ``` 
    <UseMaui>true</UseMaui>
    <-- for iOS project head -->
    <TargetFrameworks>net6.0-ios</TargetFrameworks>
    <-- for Android project head -->
    <TargetFrameworks>net6.0-android</TargetFrameworks>
    <OutputType>Exe</OutputType>
    ```
  - Copy over the project reference to the .NET MAUI Project using the old csproj file `ProjectReference` which remains the same. For example see Line 28 [here](https://github.com/Sweekriti91/ArtAuction/blob/maui-projecthead/ArtAuction.Android/ArtAuction.Android.csproj#L28) which was copied over exactly from the old `csproj`.

### Step 2: source code updates

- In the .NET MAUI project, add a new file called `MauiProgram.cs` and add the code for the `MauiAppBuilder` by referencing [this file](https://github.com/Sweekriti91/ArtAuction/blob/maui-projecthead/ArtAuction/MauiProgram.cs). More information on App Startup in the official [documentation](https://docs.microsoft.com/en-us/dotnet/maui/fundamentals/app-startup).
- In the .NET MAUI Android project, add `MainApplication.cs` if you didn't have one or edit your preexisting file to match [this file](https://github.com/Sweekriti91/ArtAuction/blob/maui-projecthead/ArtAuction.Android/MainApplication.cs) and edit `MainActivity.cs` to inherit from `MauiAppCompatActivity` to match [this file](https://github.com/Sweekriti91/ArtAuction/blob/maui-projecthead/ArtAuction.Android/MainActivity.cs).
- In the .NET MAUI Android project, update the `AndroidManifest` to `android:targetSdkVersion="31"`
- In the .NET MAUI iOS project, update `AppDelegate.cs` to inherit from `MauiUIApplicationDelegate` and match [this file](https://github.com/Sweekriti91/ArtAuction/blob/maui-projecthead/ArtAuction.iOS/AppDelegate.cs).
- In the .NET MAUI iOS project, update `Info.plist` `MinimumOSVersion` to `15.2`.
- In all 3 project heads, delete or comment out contents of the `AssemblyInfo.cs` files, you can reenable properties them once you have a version of the full app building and running without errors. Most of these properties are now `csproj` properties as part of the new .NET MAUI `csproj` so be sure to check which ones you still need.

- Global namespace updates, do a find and replace (best done in VSCode) for the following namespace changes:

    | Old namespace | New namespace |
    | --- | --- |
    | `xmlns="http://xamarin.com/schemas/2014/forms"` | `xmlns="http://schemas.microsoft.com/dotnet/2021/maui"` |
    | `using Xamarin.Forms` | `using Microsoft.Maui` **AND** `using Microsoft.Maui.Controls` |
    | `using Xamarin.Forms.Xaml` | `using Microsoft.Maui.Controls.Xaml` |
    | `using Xamarin.Essentials` | `using Microsoft.Maui.Essentials` |

- New spacing defaults for layouts can be found here: https://github.com/dotnet/maui/issues/4594

- Known API changes, check the Migrating documents per perview version on the right side navigation of this Wiki. Few common ones you will see while migrating: 
   - `Colors` and `Shapes` are in `Microsoft.Maui.Graphics`
   - `Color.Default` DOES NOT EXIST == use null instead (GitHub [Issue](https://github.com/dotnet/upgrade-assistant/issues/592))
   - `Color` == `Colors` For example: `Colors.Red;`
   - `Frame`: `BorderColor`= "Accent" DOES NOT EXIST
   - `ToolbarItem`: `Icon` == `IconImageSource`
   - `Button`: `Image` == `ImageSource`
   - `Span` `ForegroundColor` DOES NOT EXIST

- XAML updates for Layouts, check the [documentation](https://docs.microsoft.com/en-us/dotnet/maui/user-interface/layouts/relativelayout#:~:text=The.NET%20Multi-platform%20App%20UI%20%28.NET%20MAUI%29%20RelativeLayout%2C%20which,be%20created%20that%20scale%20proportionally%20across%20device%20sizes).

An example of update to be made, `AbsoluteLayout`, `RelativeLayout`,code change:

```c# 
<-- Xamarin.Forms code -->
   
<RelativeLayoutHorizontalOptions="End">
    <Switch
        x:Name="AutofillServiceSwitch"
        IsToggled="{Binding AutofillServiceToggled}"
        StyleClass="box-value"
        HorizontalOptions="End"/>
    <Button
        Clicked="ToggleAutofillService"
        StyleClass="box-overlay"
        RelativeLayout.XConstraint="0"
        RelativeLayout.YConstraint="0"
        RelativeLayout.WidthConstraint="{ConstraintExpression Type=RelativeToView, ElementName=AutofillServiceSwitch, Property=Width}"
        RelativeLayout.HeightConstraint="{ConstraintExpression Type=RelativeToView, ElementName=AutofillServiceSwitch, Property=Height}"/>
</RelativeLayout>

<-- .NET MAUI code --> 
<-- Add new XAML namespace : xmlns:compat="clr-namespace:Microsoft.Maui.Controls.Compatibility;assembly=Microsoft.Maui.Controls" -->

<compat:RelativeLayout  HorizontalOptions="End">
    <Switch
        x:Name="AutofillServiceSwitch"
        IsToggled="{Binding AutofillServiceToggled}"
        StyleClass="box-value"
        HorizontalOptions="End" />
    <Button
        Clicked="ToggleAutofillService"
        StyleClass="box-overlay"
        compat:RelativeLayout.XConstraint="0"
        compat:RelativeLayout.YConstraint="0"
        compat:RelativeLayout.WidthConstraint="{compat:ConstraintExpression  Type=RelativeToView, ElementName=AutofillServiceSwitch, Property=Width}"
        compat:RelativeLayout.HeightConstraint="{compat:ConstraintExpression  Type=RelativeToView, ElementName=AutofillServiceSwitch, Property=Height}" />
</compat:RelativeLayout>
```

### Step 3: nugets updates

- Delete `Xamarin.Forms` and `Xamarin.Essentials` nuget references
- Replace `Xamarin.Community Toolkit` with latest preview of [.NET MAUI Community Toolkit](https://github.com/CommunityToolkit/Maui)
- Replace `SkiaSharp` with latest preview: 
   - [SkiaSharp.Views.Maui.Controls](https://www.nuget.org/packages/SkiaSharp.Views.Maui.Controls/2.88.0-preview.232)
   - [SkiaSharp.Views.Maui.Core](https://www.nuget.org/packages/SkiaSharp.Views.Maui.Core/2.88.0-preview.232)
   - [SkiaSharp.Views.Maui.Controls.Compatibility](https://www.nuget.org/packages/SkiaSharp.Views.Maui.Controls.Compatibility/2.88.0-preview.232)

_more information coming soon, watch this space_ 👀🤓

### Step 4: Manually fix other build errors via IDE

After these changes, you can now open your `main sln` file in VS2022 or VSM and continue to make fixes. A good way to start would be to build the project and work through file by file fixing errors as you go. Please use the sample projects as guidelines as needed.

Another great resource would be this [repo](https://github.com/jsuarezruiz/mvpsummit2022-dotnet-maui).

For example, a common type of error seen is ambiguous like:
`error CS0104: 'ViewExtensions' is an ambiguous reference between 'Microsoft.Maui.Controls.ViewExtensions' and 'Microsoft.Maui.ViewExtensions'` which can be fixed via explicit path or alias-ing.

Once the projects compile, run the migrated projects via `dotnet cli` use the following commands : ( `-t:Run` will run the app, so to only build, remove that from the command)
  - iOS : `dotnet build <path_to_iOS_csproj_file> -f net6.0-ios -c Debug -t:Run`
  - Android: `dotnet build <path_to_Android_csproj_file> -f net6.0-ios -c Debug -t:Run`

> Most of the source code fixes would be more `using` statement fixes, explicitly qualify certain keywords and other smaller fixes.

_more updates coming soon, watch this space_ 👀 🤓

## Migration [Feedback](https://github.com/maddymontaquila/maui-migration-samples/issues/new?assignees=&labels=&template=trial-migration-template.md&title=[MIGRATION]+Your+migration+name+here)

Please File Issues [here](https://github.com/maddymontaquila/maui-migration-samples/issues/new?assignees=&labels=&template=trial-migration-template.md&title=[MIGRATION]+Your+migration+name+here), we want to hear good news, bad news, any rants, all issues, basically everything! 😁😁

Please provide us with all [the feedback](https://github.com/maddymontaquila/maui-migration-samples/issues/new?assignees=&labels=&template=trial-migration-template.md&title=[MIGRATION]+Your+migration+name+here) around migration or even if we have steps missing in the manual migration guide. The issue has a template to make providing [feedback](https://github.com/maddymontaquila/maui-migration-samples/issues/new?assignees=&labels=&template=trial-migration-template.md&title=[MIGRATION]+Your+migration+name+here) to us super easy. If you have a migrated sample and it is OSS, please let us know and we can include it in the samples linked here. All samples provided will be the test sample set for upgrade-assistant. The more we can teach the tool, the easier migrations will get! 😇

# [WIP] .NET Upgrade Assistant Steps

At this time the .NET Upgrade Assistant will do the first few steps for you. Be aware, this tool is incomplete. Please [file feedback](https://github.com/maddymontaquila/maui-migration-samples/issues/new?assignees=&labels=&template=trial-migration-template.md&title=[MIGRATION]+Your+migration+name+here) so we can improve the tool for everyone!

## Get Started

> Use source control! The assistant will try to make a backup for you, but please take care.

Install the .NET Upgrade Assistant dotnet tool: 
.com/dotnet/upgrade-assistant/issues) so we can improve the tool for everyone!

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
