In this document you will learn that:

* you do NOT need to rewrite your Xamarin.Forms application
* you WILL need to make a few code changes
* you CAN use "single project" features without merging all your projects into one
* you SHOULD wait to migrate production applications

## The Migration Vision

When we release migration guides later in 2021, we expect your steps will look something like this:

1. Run .NET Upgrade Assistant for .NET MAUI to migrate your csproj to SDK Style, and perform well known code migration (namespaces, name changes)
2. Update dependencies to .NET 6 and .NET MAUI compatible versions
3. Register any compatibility services or renderers
4. Build and fix any issues
5. Run the converted app and verify

## Porting Samples Today

As we validate our progress, we are porting Xamarin.Forms sample code and projects by hand. Below is a typical process.

Samples are almost always pure Xamarin.Forms code and have little or no custom renderers, so a new project is easiest to start with.

Let's migrate [Button Demos](https://github.com/xamarin/xamarin-forms-samples/tree/master/UserInterface/ButtonDemos)

```console
> dotnet new maui -n ButtonDemos
```

This creates a blank, multi-targeted project.

```console
> cd ButtonDemos
> dotnet restore
```

> If you are unable to restore, check the [Getting Started guide]() and make sure you have the required NuGet sources.

Now copy the [code files](https://github.com/xamarin/xamarin-forms-samples/tree/master/UserInterface/ButtonDemos/ButtonDemos/ButtonDemos) (except App.xaml) into your project.

Open the folder in your favorite code editor, and do a Find and Replace for the namespaces.

* `using Xamarin.Forms` &raquo; `using Microsoft.Maui` and `using Microsoft.Maui.Controls`
* `using Xamarin.Forms.Xaml` &raquo; `using Microsoft.Maui.Controls.Xaml`

Disable the compatibility renderers in `Startup.cs` by passing `false` to `UseFormsCompatibility`. This ensures we will be using the .NET MAUI `Button`.

Make sure you have an emulator, simulator, or device up and running. Follow the instructions in [Getting Started]() to run for a specific platform. Let's run on Android:

```console
> dotnet build -t:Run -f net6.0-android
```

Look for runtime errors.