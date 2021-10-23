## ApplicationVersion 

The versioning is now a single value that we translate to each platform. In your csproj file remove the AndroidVersion and update your ApplicationVersion.

```
<!-- Versions -->
<ApplicationVersion>1</ApplicationVersion>
```

## Mac Catalyst 

Remove the **LSMinimumSystemVersion** from the `info.plist` file.

```
<key>LSMinimumSystemVersion</key>
<string>10.15</string>
```