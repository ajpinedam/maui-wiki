It's possible to specify which simulator is launched and used for `net6.0-ios` by specifying the `_DeviceName` MSBuild property:

```console
$ dotnet build -t:Run -f net6.0-ios -p:_DeviceName=:v2:udid=<UDID>
```

You can get a list of possible UDID values by executing the `simctl list` command:

ie: `/Applications/Xcode.app/Contents/Developer/usr/bin/simctl list`

If you do not specify a UDID, you'll end up with the default iOS simulator which is mostly likely an iPad or iPod. 🤷‍♀️
