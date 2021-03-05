The list of handler properties which are ready for porting is [here](https://github.com/dotnet/maui/projects/4).

Example PR (handling Padding for Label): https://github.com/dotnet/maui/pull/421

## PRs for handler properties should:

- target a single property for a single control where possible
- implement the handler method for both iOS and Android
- reuse existing extension methods where appropriate/possible
- port the existing renderer logic where appropriate/possible
- include device tests for both iOS and Android
- avoid any changes not essential to the handler property (including whitespace)

## Tests
At a minimum, device tests should verify that the cross-platform property value translates to a reasonable native property value. 

In some cases, properties might be interrelated in a way that makes sense to implement both in a single PR; e.g., LineBreakMode and MaxLines, which affect each other on some platforms. In that case, multiple properties are fine; the goal is just to keep the PRs small and easy to review.

## Supported OS versions
When porting renderer code from Forms, keep in mind that the minimum native support levels are API 21 for Android and iOS 9. So any code that worries about API levels/versions below those can be removed.

## Ready to start?

Join us on the #maui channel on the [.NET Discord Server](http://aka.ms/dotnet-discord) and let us know what you're starting to work on so we can assign the issue to you on GitHub!  We'll also try and help answer any questions as you start coding!

## What should my PR do?

Here's the basic list of things you need to do in order to port a property from renderers to handlers:

- Add the property to the appropriate interface
- Add the mapping to the PropertyMapper in the handler
- Add the mapping method to the Android, iOS, and Standard aspects of the handler
	- Note that Standard is just a placeholder; only the platform methods actually run
- Implement the actual property updates (usually in extension methods in the Platform section of Core)	
	- The implementation details can be found in the renderers for the respective platforms
	- Again, Standard is a placeholder; you can leave these methods empty
- Implement basic property tests in DeviceTests
	- You'll need to add the new property on the device test stub class
	- If you can make the tests work in the xplat class, yay! If not, it's fine to have all or part of them on the individual platform aspects. 