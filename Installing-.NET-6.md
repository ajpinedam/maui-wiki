# Path to Success

1. Uninstall any .NET 6 workload previews using this script:  
   https://github.com/Redth/dotnet-maui-check/blob/main/Clean-Old-DotNet6-Previews.ps1
2. Uninstall any .NET 6 versions you can just to be safe
3. Install .NET 6 RC 1  
   Win: https://dotnetcli.azureedge.net/dotnet/Sdk/6.0.100-rc.1.21418.8/dotnet-sdk-6.0.100-rc.1.21418.8-win-x64.exe   
   macOS: https://dotnetcli.azureedge.net/dotnet/Sdk/6.0.100-rc.1.21418.8/dotnet-sdk-6.0.100-rc.1.21418.8-osx-x64.pkg  
   > I just use maui-check to install .NET, but not the workloads.  
   > Run and then when it asks to install .NET, go ahead and then when it asks to install workloads, just cancel.
4. Install the workloads individually: `android-aot`, `ios`, `maccatalyst`, `macos`, `tvos`  
   This is due to this bug: https://github.com/dotnet/sdk/issues/19739  
   Use the source: `--source https://aka.ms/dotnet/maui/main/index.json`
5. Install maui: `dotnet workload maui --source https://aka.ms/dotnet/maui/main/index.json`
6. Profit