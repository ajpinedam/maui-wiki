## What is .NET MAUI?

.NET MAUI is the Multi-platform App UI for building native cross-platform apps with .NET for Android, iOS, macOS, and Windows. It is the evolution of Xamarin.Forms, taking its place as the .NET solution for building native cross-platform apps.

## When will .NET MAUI be available?

We expect to begin shipping previews near the end of 2020. MAUI will hit general availability (GA) in November 2021 when .NET 6 ships.

## Will MAUI support XAML and MVVM?

Absolutely! As an evolution of Xamarin.Forms, you will be able to use all XAML with all its existing features and we will continue to improve XAML to help you be even more productive. MAUI will continue to support MVVM while providing developers options to use RxUI and MVU.

## What is the future of Xamarin.Forms?

The next major version of Xamarin.Forms will around September 2020 and continue to be updated through the release of MAUI with .NET 6. After that, Xamarin.Forms will continue to receive priority servicing for 12 months.

## Should I upgrade my Xamarin.Forms applications to .NET MAUI?

Initially, we recommend you explore MAUI on new projects. We are working to make the transition from existing projects as seamless as possible as you will enjoy project system improvements, a new .NET, and a new renderer architecture in MAUI.

## Why is Xamarin.Forms becoming .NET MAUI?

We are unifying the .NET platform! As with all key workloads and runtimes of .NET, we are closely integrating Xamarin.Forms and Xamarin.Essentials, and the Android, iOS, and macOS bindings into .NET. This is clearly illustrated by the namespace changes: `Xamarin.Forms` becomes `System.Maui` and `Xamarin.Essentials` becomes `System.Devices`. 

## What is MVU?

MVU stands for Model-View-Update, an application architecture popular in the [Elm](https://elmprogramming.com/model-view-update-part-1.html) programming language and first demonstrated as a powerful option for Xamarin.Forms in the F# implementation, [Fabulous](https://fsprojects.github.io/Fabulous/Fabulous.XamarinForms/). Due to the single flow of state in this architecture, things like hot reload become much easier to fully implement.

## Do I have to use MVU?

Not at all! You have a choice to use what makes you most productive and makes the most sense for your application, whether that's MVVM, MVU, or another architecture of your choice. The same goes for XAML and C#, both are fully supported ways to build the UI for your apps.

## What is RxUI?

RxUI stands for [ReactiveUI](https://reactiveui.net/), a functional and [reactive](https://reactiveui.net/docs/reactive-programming/) MVVM framework for building .NET applications.  