For a current status on the progress of porting controls, features, and layouts from Xamarin.Forms to .NET MAUI, visit the [status report](https://github.com/dotnet/maui/wiki/status).

# Upcoming Milestones

## **.NET MAUI in .NET 6 Preview 7 (August 2021)**

Updated:
* [AppThemeBinding](https://github.com/dotnet/maui/pull/1657)
* [Layouts](https://github.com/dotnet/maui/issues/1592) - removing shimmed layouts
* [Native Application Lifecycle Events](https://github.com/dotnet/maui/issues/1582)
* [Frame](https://github.com/dotnet/maui/pull/787)

## **.NET MAUI in .NET 6 Release Candidate (September 2021)**

Planned:
* Bug fixes
* [Borders](https://github.com/dotnet/maui/pull/650)
* [Corners](https://github.com/dotnet/maui/pull/650)
* [Shadows](https://github.com/dotnet/maui/pull/570)

## **.NET MAUI in .NET 6 Release Candidate (October 2021)**

Planned:
* Bug fixes
* [Cross-platform Lifecycle Events](https://github.com/dotnet/maui/issues/1721)

## **.NET MAUI General Availability (November 2021)**

Planned:
* Bug fixes


## **Deferred from .NET 6 GA**

The following work was originally planned for .NET 6 GA, and through ongoing prioritization has been deferred. 

* Mult-window desktop implementation - the API and foundation is present, ready for implementation
* Drawn Design System components - Fluent UI and Material Design themed components you can use with the `Visual` API. This replaces the cut Material Design for iOS components based on the Google library
* Handlers for CarouselView, CollectionView, IndicatorView, RefreshView, SwipeView, TabbedPage, and FlyoutPage. These are available using existing renderers 
* [Native Embedding (Context factory)](https://github.com/dotnet/maui/issues/1718)
