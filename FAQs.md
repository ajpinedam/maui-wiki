## What is .NET MAUI?

.NET MAUI is the Multi-platform App UI for building native cross-platform apps with .NET for Android, iOS, macOS, and Windows. It is the evolution of Xamarin.Forms, taking its place as the .NET solution for building native cross-platform apps.

## When will .NET MAUI be available?

See the [.NET MAUI Roadmap](https://github.com/dotnet/maui/wiki/Roadmap) for details.

## Will .NET MAUI support XAML and MVVM?

Absolutely! As an evolution of Xamarin.Forms, you will be able to use all XAML with all its existing features and we will continue to improve XAML to help you be even more productive. .NET MAUI will continue to support MVVM while providing developers options to use RxUI and MVU.

## Should I upgrade my Xamarin.Forms applications to .NET MAUI?

Initially, we recommend you explore .NET MAUI on new projects. We are working to make the transition from existing projects as seamless as possible as you will enjoy project system improvements, a new .NET, and a new architecture in .NET MAUI.

## Will my Xamarin.Forms projects automatically update to .NET MAUI?

See our [migration guide here](https://docs.microsoft.com/en-us/dotnet/maui/get-started/migrate).

## Why is Xamarin.Forms becoming .NET MAUI?

We are unifying the .NET platform! As with all key workloads and runtimes of .NET, we are closely integrating Xamarin.Forms and Xamarin.Essentials, and the Android, iOS, and macOS bindings into .NET. This is clearly illustrated by the namespace changes: `Xamarin.Forms` becomes `Microsoft.Maui` and `Xamarin.Essentials` becomes `Microsoft.Maui.Essentials`. 

##  Will .NET MAUI allow deployment of one code base across Android, iOS, macOS, and Windows?

Yes, check out [this chart in the README](https://github.com/dotnet/maui#xamarinforms-vs-net-maui) to see the supported platforms.

## What "flavor" of XAML will be supported by .NET MAUI?

.NET MAUI uses the same XAML as Xamarin.Forms.

## How will .NET MAUI affect existing Xamarin Plugins developed by the community?

To target it, NuGet Packages will need to add a dependency to .NET 6 and reference the new namespaces.

## Will .NET MAUI allow you to break out into Native UI when needed?

Yes, it leverages [Multitargeting](https://docs.microsoft.com/visualstudio/mac/project-multitargeting?WT.mc_id=maui-github-bramin) which allows you to reference platform-specific APIs in a unified .NET MAUI project

 ![Platform Specific Libraries](https://codetraveler.io/content/images/2020/05/Picture1.png)
 