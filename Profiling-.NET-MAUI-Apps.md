
## Local .NET SDK

For most cases when testing PRs or even just for consistency, use the local "install" of dotnet. This can be built using:

```
dotnet build src/DotNet/DotNet.csproj
```

> In order to use custom packages from a PR:
> - make sure the packages exist in an `artifacts` directory at the root
> - update the `eng/Versions.props` file to that version
> - uncomment the `<add key="local" value="artifacts" />` in the `NuGet.config` at the root

## Required Tools

Profiling .NET apps require a few tools:

 - `dotnet tool update -g dotnet-dsrouter --add-source=https://aka.ms/dotnet-tools/index.json`
 - `dotnet tool update -g dotnet-trace --add-source=https://aka.ms/dotnet-tools/index.json`

### `dotnet-dsrouter`

The first part that is required is `dotnet-dsrouter`, which routes traffic from the emulator/device to a socket.

```
dotnet-dsrouter client-server -tcps 127.0.0.1:9001 -ipcc /tmp/maui-app --verbose debug
```

This command sets up the router to route data from `127.0.0.1:9001` to `/tmp/maui-app`.

### `dotnet-trace`

The next part is the trace tool, which reads data from the socket into a file once the app has launched.

```
dotnet-trace collect --diagnostic-port /tmp/maui-app --format speedscope -o maui-app-trace
```

This commands converts the trace data into a file from `/tmp/maui-app` to a `maui-app-trace.json` file.

Each time the app is launched, the tool will have to be run. Once enough data has been collected, press `Enter`. This will terminate the trace app and create the trace output file at `maui-app-trace.json`.

## Running the Profiler

Once both tools are running and ready to go, the app can be launched.

To build the profiling app from source, use the local dotnet instance:

```
./bin/dotnet/dotnet build src/Controls/samples/Controls.Sample.Profiling -f net6.0-android -t:run -c Release -p:IsEmulator=true
```

This builds the app and runs it on the device/emulator.

The `IsEmulator` property can be used to control the environment variables of the app. The main reason is that it uses different ports on the Android device depending on whether it is a local emulator or a connected device.

> You may have to build the build tasks for the first run:  
> ```
>  ./bin/dotnet/dotnet build Microsoft.Maui.BuildTasks-net6.slnf
> ```

### Physical Devices

If a physical device is to be used, then there needs to be a port opened on the Android device via adb:

```
adb reverse tcp:9000 tcp:9001
```

This commands forwards port `9000` from the device to port `9001` on the host machine.

The same run command can be used for emulators, except that the `IsEmulator` property should be set to `false`.

## Viewing the results

Once you finish the profiling, there will be a json file named `maui-app-trace.json` that can be viewed online at: https://www.speedscope.app/

Or, you can use PerfView: https://github.com/microsoft/perfview/releases

Or you can try open it in VS.


## Troubleshooting

* If there is broken/missing information in the traces, make sure you are _not_ using the interpreter. Remove the `<UseInterpreter>` element (or set it to `false`).