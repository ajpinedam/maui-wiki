# Path to Success

1. Uninstall any .NET 6 workload previews using this script:  
   https://github.com/Redth/dotnet-maui-check/blob/main/Clean-Old-DotNet6-Previews.ps1
2. Uninstall any .NET 6 versions you can just to be safe
3. Install .NET 6 RC 1  
   Win: https://dotnetcli.azureedge.net/dotnet/Sdk/6.0.100-rc.1.21424.1/dotnet-sdk-6.0.100-rc.1.21424.1-win-x64.exe   
   macOS: https://dotnetcli.azureedge.net/dotnet/Sdk/6.0.100-rc.1.21424.1/dotnet-sdk-6.0.100-rc.1.21424.1-osx-x64.pkg  
4. Delete this file: `C:\Program Files\dotnet\metadata\workloads\6.0.100\installertype\msi`
5. Install the workloads individually: `android-aot`, `ios`, `maccatalyst`, `macos`, `tvos`  
   This is due to this bug: https://github.com/dotnet/sdk/issues/19739  
   Use the source: `--source https://aka.ms/dotnet/maui/rc1/index.json`
6. Install maui: `dotnet workload install maui --source https://aka.ms/dotnet/maui/rc1/index.json`
7. Make sure to remove all previous Reunion extensions
8. Install the VS extension:  
   https://marketplace.visualstudio.com/items?itemName=ProjectReunion.MicrosoftSingleProjectMSIXPackagingToolsDev17
9. Profit