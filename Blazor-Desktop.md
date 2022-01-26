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
| [sample](https://github.com/dotnet/maui/tree/main/src/BlazorWebView/samples/BlazorWinFormsApp) | [sample](https://github.com/dotnet/maui/tree/main/src/BlazorWebView/samples/BlazorWpfApp) | [sample code](https://github.com/dotnet/maui/tree/main/src/Controls/samples/Controls.Sample), and [sample app](https://github.com/dotnet/maui/tree/main/src/Controls/samples/Controls.Sample.SingleProject) |
| - | - | [tests](https://github.com/dotnet/maui/tree/main/src/BlazorWebView/tests/MauiDeviceTests) |

## BlazorWebView

The main component on each platform is the `BlazorWebView` control. They each have a unique implementation in the source locations above, though they do use some [shared source](https://github.com/dotnet/maui/tree/main/src/BlazorWebView/src/SharedSource) for Windows/WebView2 related code.

# Teams Channel (Microsoft internal)

Go to [this channel](https://teams.microsoft.com/l/channel/19%3a989ffa44998147aca4ceaf7482967668%40thread.skype/MAUI%2520%25F0%259F%258C%25BA?groupId=0056f60b-301f-43ac-bbcf-f356d3c42c92&tenantId=72f988bf-86f1-41af-91ab-2d7cd011db47) (and request to join if you don't have access).

# Getting Started working on Blazor Hybrid brownbag (Microsoft internal)

Watch the [recording of a brownbag session](https://microsoft-my.sharepoint.com/:v:/r/personal/jacalvar_microsoft_com/Documents/Recordings/Brownbag_%20Getting%20started%20with%20Blazor%20Hybrid-20220125_103336-Meeting%20Recording.mp4?csf=1&web=1&e=Z4j796) on working on Blazor Hybrid (Microsoft internal)