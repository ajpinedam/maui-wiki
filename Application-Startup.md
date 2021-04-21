New .NET MAUI apps use HostBuilder from Microsoft.Extensions to bootstrap. In addition to initializing the bare minimum you need for a quick start, it also provides a single point to configure fonts, services, third-party libraries, and register for backward compatibility features.

## Startup Flow

Each native platform has a different starting point that initializes the app host builder, and at the end calls `Startup`. This is where your application development begins.

## Minimal Startup

At a minimum you will provide an application to run.

```csharp
public class Startup : IStartup
{
    public void Configure(IAppHostBuilder appBuilder)
    {
        appBuilder
            .UseMauiApp<App>();
    }
}
```

Your `App` is an implementation of `Application` and it provides a `Window` within which your app runs.

```csharp
public partial class App : Application
{
    public override IWindow CreateWindow(IActivationState activationState)
    {
        return new MainWindow();
    }
}
```

Your `MainWindow` takes any view content and has a context to manage state. This context also has its own navigation stack. We'll cover more about this when we introduce multi-window support. For now, we'll add a `ContentPage` to `MainWindow`.

```csharp
public class MainWindow : IWindow
{
    public MainWindow()
    {
        Page = new MainPage();
    }

    public IPage Page { get; set; }

    public IMauiContext MauiContext { get; set; }
}
```

And with that you have a minimal application that'll run and display whatever you put into `MainPage`.

## Registering Fonts

You can easily add fonts to your .NET MAUI application and reference them by filename, but if you want to add a convenient alias then you'll want to register that alias.

```csharp
appBuilder
    .UseMauiApp<App>()
    .ConfigureFonts(fonts => {
        fonts.AddFont("ionicons.ttf", "IonIcons");
    })
```

> Note: when adding font files, you'll want to include them in your csproj using a wildcard or the specific filename:
> ```  
> <ItemGroup>
>    <MauiFont Include="Resources\Fonts\*" />
>  </ItemGroup>
> ```

## Configuring Essentials

```csharp
appBuilder
    .UseMauiApp<App>()
    .ConfigureEssentials(essentials =>
    {
        essentials
            .UseVersionTracking()
            .UseMapServiceToken("YOUR-KEY-HERE");
    });
```

## Configuring Compatibility

To use the Xamarin.Forms legacy controls backed by renderers instead of handlers, you can call `UseFormsCompatibility()`. This will default to those controls. By passing in `false` you can use all Xamarin.Forms compatibility features **except for** renderers, and then use the `ConfigureMauiHandlers` extension method to register specific renderers. All other controls will use the new .NET MAUI controls backed by handlers.

```csharp
appBuilder
    .UseFormsCompatibility(false)
    #if __ANDROID__
    .ConfigureMauiHandlers(handlers => {
        handlers.AddCompatibilityRenderer(typeof(Microsoft.Maui.Controls.BoxView), 
            typeof(Microsoft.Maui.Controls.Compatibility.Platform.Android.BoxRenderer));
        handlers.AddCompatibilityRenderer(typeof(Microsoft.Maui.Controls.Frame), 
            typeof(Microsoft.Maui.Controls.Compatibility.Platform.Android.FastRenderers.FrameRenderer));	
    })
    #endif
    #if __IOS__
    .ConfigureMauiHandlers(handlers => {
        handlers.AddCompatibilityRenderer(typeof(Microsoft.Maui.Controls.BoxView), 
            typeof(Microsoft.Maui.Controls.Compatibility.Platform.iOS.BoxRenderer));
        handlers.AddCompatibilityRenderer(typeof(Microsoft.Maui.Controls.Frame), 
            typeof(Microsoft.Maui.Controls.Compatibility.Platform.iOS.FrameRenderer));
        handlers.AddCompatibilityRenderer(typeof(Microsoft.Maui.Controls.ScrollView), 
            typeof(Microsoft.Maui.Controls.Compatibility.Platform.iOS.ScrollViewRenderer));
    })
    #endif
    .UseMauiApp<App>();
```