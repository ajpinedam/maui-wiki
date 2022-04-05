## Shell 

In order to use constructor injection with `ContentPage`s in the context of Shell, you'll need to register them with DI just like you have your view models.

## Blazor

* Use `services.AddMauiBlazorWebview()` instead of `builder.RegisterBlazorMauiWebView()` and `services.AddBlazorWebView()` to register Blazor Webview in Maui applications. Calling `services.AddBlazorWebView()` is no longer necessary since it's done as part of `services.AddMauiBlazorWebview()`

## Renames

* occurrences of "native" have been replaced with "platform"
* `OSAppTheme` is now `AppTheme`

## Type Changes

`Rectangle` to `Rect`

## OnPlatform Changes

The available platforms are now:

- Android
- iOS
- MacCatalyst
- Tizen
- WinUI
