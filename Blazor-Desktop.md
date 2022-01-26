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
