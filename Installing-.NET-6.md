1. Uninstall any .NET 6 versions and workload previews using this script:  
   https://github.com/Redth/dotnet-maui-check/blob/main/Clean-Old-DotNet6-Previews.ps1  
   This is just in case maui-check installed an conflicting version some time ago. You won't be able to uninstall version installed by VS, but this is fine to ignore. It is more to remove the versions before preview 7.
1. Install .NET 6 RC 1  
   Win: https://dotnetcli.azureedge.net/dotnet/Sdk/6.0.100-rc.1.21426.23/dotnet-sdk-6.0.100-rc.1.21426.23-win-x64.exe   
   macOS: https://dotnetcli.azureedge.net/dotnet/Sdk/6.0.100-rc.1.21426.23/dotnet-sdk-6.0.100-rc.1.21426.23-osx-x64.pkg  
1. Delete this file: `C:\Program Files\dotnet\metadata\workloads\6.0.100\installertype\msi`
1. Install the workloads individually: `android-aot`, `ios`, `maccatalyst`, `macos`, `tvos`  
   This is due to this bug: https://github.com/dotnet/sdk/issues/19739  
   Use the source: `--source https://aka.ms/dotnet/maui/rc1/index.json`
   > IMPORTANT FOR TVOS: Right at this second, the system is in a transitional phase and we are waiting on a build from iOS to push all the correct RC 1 bits into the feeds. Until then, there is a bit of work to do this:  
   >  a) You will have to use a local folder feed with a few specific packages that you need to download from the xamarin-impl feed:  
   >     *  https://dev.azure.com/azure-public/vside/_packaging?_a=package&feed=xamarin-impl&package=Microsoft.tvOS.Ref&protocolType=NuGet&version=15.0.100-rc.1.521%2Bsha.453791f44&view=overview  
   >     *  https://dev.azure.com/azure-public/vside/_packaging?_a=package&feed=xamarin-impl&package=Microsoft.tvOS.Runtime.tvos-arm64&protocolType=NuGet&version=15.0.100-rc.1.521%2Bsha.453791f44&view=overview  
   >     *  https://dev.azure.com/azure-public/vside/_packaging?_a=package&feed=xamarin-impl&package=Microsoft.tvOS.Runtime.tvossimulator-x64&protocolType=NuGet&version=15.0.100-rc.1.521%2Bsha.453791f44&view=overview  
   >     *  https://dev.azure.com/azure-public/vside/_packaging?_a=package&feed=xamarin-impl&package=Microsoft.tvOS.Sdk&protocolType=NuGet&version=15.0.100-rc.1.521%2Bsha.453791f44&view=overview  
   >     *  https://dev.azure.com/azure-public/vside/_packaging?_a=package&feed=xamarin-impl&package=Microsoft.tvOS.Templates&protocolType=NuGet&version=15.0.100-rc.1.521%2Bsha.453791f44&view=overview  
   >  b) Copy the 5 .nupkg files into a folder that does not have any other versions of dotnet packages  
   >  c) Add an **additional** `--source /path/to/folder` to `dotnet workload install` commands
1. Install maui: `dotnet workload install maui --source https://aka.ms/dotnet/maui/rc1/index.json`
1. Make sure to **remove all previous** Reunion extensions and install the new one:  
   https://marketplace.visualstudio.com/items?itemName=ProjectReunion.MicrosoftSingleProjectMSIXPackagingToolsDev17
