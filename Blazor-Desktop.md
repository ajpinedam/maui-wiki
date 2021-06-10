# Blazor Desktop

1. Install required .NET MAUI dependencies using the `maui-check` tool as described in the [samples repo](https://github.com/dotnet/maui-samples#installing-with-net-maui-check-tool).
1. Use one of the following solutions to build the code or run the samples:
   - `BlazorWindows-net6.sln`: For .NET MAUI WinUI, WPF, and Windows Forms
   - `BlazorNonWindows-net6.sln`: For .NET MAUI Android, iOS, and Mac Catalyst
   - Note: The `BlazorWindowsDesktop-net6.sln` solution is for CI/build purposes only.
1. To change the samples to use Blazor UI instead of native UI, edit these files:
   - For multi-project samples, edit `src/Controls/samples/Controls.Sample/Startup.cs` and set `_pageType = PageType.Blazor`
   - For single-project samples, edit `src/Controls/samples/Controls.Sample.SingleProject/Startup.cs` and set `UseBlazor = true`
