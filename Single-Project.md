# Single Project
Single Project is a collection of features that brings all the platform-specific experiences developers encounter while developing client applications into one shared head project that can target Android, iOS, Windows, and Mac (using Mac Catalyst).

Single Project is enabled using multi-targeting and the use of SDK-style projects in .NET 6. You can still expect access to all the platform-specific experiences and tools when you need them, while enjoying a simplified, shared development experience across all the platforms you're targeting.

## Experiences Simplified
Single Project is built on top of a collection of experiences that are being simplified in .NET 6. Below is an itemized list of experiences that will be shared in Single Project.
* Resources
  * Images
  * Fonts
  * Application Icons
  * Splash Screens
  * Raw Assets
* Application Manifest
* NuGet 
* Platform-Specific Code

All other features are being moved from their own platform-projects into platforms folders.

## Visual Studio Changes
In addition to the simplified, shared experiences in Single Project, there are changes being made to Visual Studio to support these changes. These changes will enable the use of a shared resource file within the shared project, platform files for platform-specific development, and a simplified debug target selection for running your .NET MAUI Application.
