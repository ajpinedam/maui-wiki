# Development

1. Install required .NET MAUI dependencies described in the [.NET MAUI Development Guide](https://github.com/dotnet/maui/blob/main/.github/DEVELOPMENT.md).
1. Follow the other instructions on that guide for how to build, open the solution, etc.
1. On VS Windows use the `Microsoft.Maui-net6.sln` solution, and on VS Mac use the `Microsoft.Maui-mac.slnf` solution filter

# Issue tracking

The `area/blazor 🕸️` label is used to track Blazor items: https://github.com/dotnet/maui/issues?q=is%3Aissue+is%3Aopen+label%3A%22area%2Fblazor+%F0%9F%95%B8%EF%B8%8F%22

This private project is used for triaging/prioritization: https://github.com/orgs/dotnet/projects/81/views/1

# Sources, samples, and tests

The Blazor-related projects in the repo are mostly located in the [src/BlazorWebView](https://github.com/dotnet/maui/tree/main/src/BlazorWebView) folder, aside from the MAUI sample app:

|  WinForms | WPF  | .NET MAUI  |
|---|---|---|
| [source](https://github.com/dotnet/maui/tree/main/src/BlazorWebView/src/WindowsForms) | [source](https://github.com/dotnet/maui/tree/main/src/BlazorWebView/src/Wpf) | [source](https://github.com/dotnet/maui/tree/main/src/BlazorWebView/src/Maui) |
| - | - | [templates](https://github.com/dotnet/maui/tree/main/src/Templates/src/templates/maui-blazor) |
| [sample](https://github.com/dotnet/maui/tree/main/src/BlazorWebView/samples/BlazorWinFormsApp) | [sample](https://github.com/dotnet/maui/tree/main/src/BlazorWebView/samples/BlazorWpfApp) | [sample code](https://github.com/dotnet/maui/tree/main/src/Controls/samples/Controls.Sample), and [sample app](https://github.com/dotnet/maui/tree/main/src/Controls/samples/Controls.Sample.SingleProject) |
| - | - | [tests](https://github.com/dotnet/maui/tree/main/src/BlazorWebView/tests/MauiDeviceTests) |

## BlazorWebView

The main component on each platform is the `BlazorWebView` control. They each have a unique implementation in the source locations above, though they do use some [shared source](https://github.com/dotnet/maui/tree/main/src/BlazorWebView/src/SharedSource) for Windows/WebView2 related code.

## ASP.NET Core

The core WebView integration with Blazor is handled within the `dotnet/aspnetcore` repo [here](https://github.com/dotnet/aspnetcore/tree/main/src/Components/WebView/WebView).

### Debugging Blazor Hybrid with experimental ASP.NET Core bits

Sometimes it may be necessary to make changes in [`dotnet/aspnetcore`](https://github.com/dotnet/aspnetcore), and react to the changes in this repo. The following are steps which outline the general process in using ASP.NET Core development `nupkg`s with MAUI.

## Steps

1. Checkout [`dotnet/aspnetcore`](https://github.com/dotnet/aspnetcore), and follow the initialization instructions in the [Build From Source](https://github.com/dotnet/aspnetcore/blob/main/docs/BuildFromSource.md) guide.
1. `./restore.cmd`
1. `. ./activate.ps1`
1. Make the desired changes in `dotnet/aspnetcore`.
1. `./eng/build.cmd -pack`. The `-pack` option causes the creation of NuGet packages.
    - Note packing the full repo is only required upon the first change. Subsequent changes are likely to be isolated in `src/Components`, hence you should be able too use `.\src\Components\build.cmd -pack`.
1. You should see the generated packages in the `aspnetcore\artifacts\packages\Debug\NonShipping` directory. The packages should end with `x.0.0-dev.nupkg` where `x` is the current (pre-release) .NET version _OR_ `y.0.patch.nupkg` where `y` is the current (released) .NET version and `patch` is the current patch version (ex. `6.0.4.nupkg`). We'll refer to the version seen here as `VERSION` in subsequent steps.
1. Open `razor-tooling/NuGet.config` and add the local package sources:

   - `dotnet nuget add source "<PATH_TO_ASPNET_CORE_REPO>\artifacts\packages\Debug\Shipping\" --name "ASPNETCORE_SHIPPING"`
   - `dotnet nuget add source "<PATH_TO_ASPNET_CORE_REPO>\artifacts\packages\Debug\NonShipping\" --name "ASPNETCORE_NONSHIPPING"`

1. Open `maui/eng/Versions.props` and update all the `MicrosoftAspNetCore*PackageVersion` and `MicrosoftJSInteropPackageVersion` to reflect the `VERSION`.

1. Go to `<USER_HOME>\.nuget\packages\microsoft.aspnetcore.components.webview` and delete the directory named `VERSION`. This clears the nuget cache.

1. Run `dotnet restore` in the directory for the app you're trying the experimental aspnetcore changes in (ex. `\src\BlazorWebView\samples\BlazorWpfApp`). 

1. You can now run the application and it'll use the experimental aspnetcore changes. Note, subsequent changes in the `aspnetcore` repo will require rebuilding (`.\src\Components\build.cmd -pack`) and repeating the previous two steps (clear nuget cache, run `dotnet restore`).


# Teams Channel (Microsoft internal)

Go to [this channel](https://teams.microsoft.com/l/channel/19%3a989ffa44998147aca4ceaf7482967668%40thread.skype/MAUI%2520%25F0%259F%258C%25BA?groupId=0056f60b-301f-43ac-bbcf-f356d3c42c92&tenantId=72f988bf-86f1-41af-91ab-2d7cd011db47) (and request to join if you don't have access).

# Getting Started working on Blazor Hybrid brownbag (Microsoft internal)

Watch the [recording of a brownbag session](https://microsoft-my.sharepoint.com/:v:/r/personal/jacalvar_microsoft_com/Documents/Recordings/Brownbag_%20Getting%20started%20with%20Blazor%20Hybrid-20220125_103336-Meeting%20Recording.mp4?csf=1&web=1&e=Z4j796) on working on Blazor Hybrid (Microsoft internal)