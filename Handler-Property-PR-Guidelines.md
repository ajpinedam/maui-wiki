The list of handler properties which are ready for porting is [here](https://github.com/dotnet/maui/projects/4).

Example PR: https://github.com/dotnet/maui/pull/421

PRs for handler properties should:

- target a single property for a single control where possible
- implement the handler method for both iOS and Android
- reuse existing extension methods where appropriate/possible
- port the existing renderer logic where appropriate/possible
- include device tests for both iOS and Android
- avoid any changes not essential to the handler property (including whitespace)

At a minimum, device tests should verify that the cross-platform property value translates to a reasonable native property value. 

In some cases, properties might be interrelated in a way that makes sense to implement both in a single PR; e.g., LineBreakMode and MaxLines, which affect each other on some platforms. In that case, multiple properties are fine; the goal is just to keep the PRs small and easy to review.

When porting renderer code from Forms, keep in mind that the minimum native support levels are API 21 for Android and iOS 9. So any code that worries about API levels/versions below those can be removed.