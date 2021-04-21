UI controls in .NET MAUI are rendered via handlers, lightweight classes that map properties and features to bite-sized implementations. Combine that with .NET multi-targeting and you can now succinctly augment any aspect of the native platform control.

> The following examples show using compiler directives (#ifdef) to multi-target code based on platform. You can just as easily use platform-specific folders or files to organize such code like `Android\Entry.cs` for `Entry` specific customizations, or `Entry.android.cs`. The organization is up to you. 

This code can live anywhere in your .NET MAUI project. 

## Example: Debug Rainbows

This would call `RandomColor` when setting the `BackgroundColor` on any view.

```csharp
#if ANDROID
Handlers.ViewHandler
    .ViewMapper[nameof(IView.BackgroundColor)] = (h, v) =>
    {
	(h.NativeView as global::Android.Views.View).BackgroundColor 
		= RandomColor();
    };
#endif
```

## Example: Remove Android Entry Underline

```csharp
#if ANDROID
Handlers.EntryHandler
    .EntryMapper[nameof(IEntry.BackgroundColor)] = (h, v) =>
    {
        (h.NativeView as global::Android.Views.Entry).UnderlineVisible = false;
    };
#endif
```

## Example: Accessibility Testing

```csharp
#if ENABLE_TEST_CLOUD
Handlers.ViewHandler
    .ViewMapper[nameof(IView.AutomationId)] = (h, v) =>
    {
        (h.NativeView as global::Android.Views.View).ContentDescription 
            = v.AutomationId;
    };
#endif
```
<!--
## Example: Mapping A Custom Property

```csharp
#if ANDROID
Handlers.EntryHandler
    .EntryMapper["Goatee"] = (h, v) =>
    {
        bool hasGoatee = (bool)v;
        if(!hasGoatee)
            (h.NativeView as global::Android.Views.Entry).UnderlineVisible = false
    };
#endif
```

Usage:

```csharp
var cleanEntry = new Entry();
```
-->
