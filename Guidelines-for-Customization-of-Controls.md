This page is intended to be a guide for users who are interested in customizing the behavior of MAUI controls for their own applications. 

## Option 1: Mappings

Mappings are the first and easiest option for most behavior changes. If you want to change how a property affects a native control (or even ignore a property), modifying the mapping for the property is the way to go. Existing mappings can be modified or replaced, and you can add brand new mappings.

For examples of modifying an existing mapping, see [Customizing Controls with Handlers](https://github.com/dotnet/maui/wiki/Customizing-Controls-with-Handlers).

```
insert example of modifying an existing mapping
```

```
insert example of adding a brand new mapping
```

## Option 2: Custom Factory Method

Each Handler type provides a factory method (`public static Func<T>`) which it uses when creating the native control. If you wish to use a custom subclass of the native control type in your handler, you can modify the factory method to return the desired type. This should only be used if the customizations you need are not achievable via a mapping (e.g., if your custom type requires particular constructor parameters).
 

```
insert example
```

## Option 2.5: Subclassing the Native Control Type

Some customizations of native controls may not be achievable via public property setters and methods; in those cases, you may need to subclass the native control type. You will also need to modify the factory method (see above) to return your custom type.

## Option 3: Creating your own Handler

Tweaking existing handlers may not be sufficient to achieve your goals - you may simply need to create your own completely custom handler. 

Maybe you need a lot of mappings that aren't available on the default handler, or you want radically different behavior. Creating your own handler is easy - here's how:

```
insert example
make sure to include host builder stuff
```

## Option 4: Subclassing a Handler

In some rare cases, you may need to subclass the handler for a control type in order to achieve the desired behavior. This should only be done when all other possibilities have been exhausted.

```
insert example
(include setting the handler in AppHostBuilder)
```

