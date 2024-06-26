# .NET

<p align="center"><img align="center" width="20%" height="20%" src="assets/dotnet.svg"></p>

[.NET](https://en.wikipedia.org/wiki/.NET) is a free and open-source, managed computer software framework for Windows, Linux, and macOS operating systems. The project is primarily developed by Microsoft employees by way of the [.NET Foundation](https://en.wikipedia.org/wiki/.NET_Foundation), and released under the MIT License.

## Index

* [Dotnet](#dotnet)
  * [Publish](#publish)
* [Worker Services](#worker-services)
* [Special Folders](#special-folders)

## Dotnet

The [dotnet](https://learn.microsoft.com/en-us/dotnet/core/tools/) command-line interface is a cross-platform toolchain for developing, building, running, and publishing .NET applications.

### Publish

The [dotnet publish](https://learn.microsoft.com/en-us/dotnet/core/tools/dotnet-publish) command publishes the application and its dependencies to a folder for deployment to a hosting system.

| Argument | Description |
|---|---|
| `-p:PublishSingleFile=true` | Packages into a single-file executable. |
| `--arch` | Target architecture.<br>`x64` |
| `--configuration` | Build configuration.<br>`Debug` `Release` |
| `--framework` | Target framework.<br>`net6.0` |
| `--output` | Output directory.<br>`Build` |
| `--os` | Target operating system.<br>`win` |
| `--self-contained` | Packages the .NET runtime with the application so the runtime doesn't need to be installed on the target machine.<br>`true` `false` |

## Worker Services

[Worker services](https://learn.microsoft.com/en-us/dotnet/core/extensions/workers) are applications that can be used to queue operations in the background, schedule operations to execute at a later time or perform processor-intensive tasks. The project template `Worker Service Template` is available in Visual Studio and dotnet CLI.

Windows services are supported worker services.
1. Install the NuGet package `Microsoft.Extensions.Hosting.WindowsServices`.
2. Modify the program to use the windows service:
```csharp
IHost host = Host.CreateDefaultBuilder(args)
    .UseWindowsService(options =>
    {
        options.ServiceName = "My Windows Service";
    })
    .ConfigureServices(services =>
    {
        services.AddHostedService<Worker>();
    })
    .Build();
```

Once the worker service is built, the windows service can be controlled using the Service Control application.

* [Create](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/sc-create)
```
sc.exe create "My Service" binpath="path/to/service.exe"
```

* Start
```
sc.exe start "My Service"
```

* Stop
```
sc.exe stop "My Service"
```

* [Delete](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/sc-delete)
```
sc.exe delete "My Service"
```

## Special Folders

[Special folders](https://learn.microsoft.com/en-us/dotnet/api/system.environment.specialfolder) are system-defined paths.
* The function `System.Environment.GetFolderPath(System.Environment.SpecialFolder)` returns the path of a special folder.
* The enum `System.Environment.SpecialFolder` is a list of special folders constants.

| Path | Name |
|---|---|
| `C:/Users/<User>/Documents` | `MyDocuments` |
| `C:/Users/<User>/Pictures` | `MyPictures` |
| `C:/Users/<User>/Music` | `MyMusic` |
| `C:/Users/<User>/Videos` | `MyVideos` |
| `C:/Users/<User>/Desktop` | `Desktop` |
| `C:/Users/<User>/Favorites` | `Favorites` |
| `C:/Users/<User>/AppData/Roaming` | `ApplicationData` |
| `C:/Users/<User>/AppData/Roaming/Microsoft/Windows/Start Menu` | `StartMenu` |
| `C:/Users/<User>/AppData/Roaming/Microsoft/Windows/Start Menu/Programs/Startup` | `Startup` |
| `C:/Users/Public/Documents` | `CommonDocuments` |
| `C:/Users/Public/Pictures` | `CommonPictures` |
| `C:/Users/Public/Music` | `CommonMusic` |
| `C:/Users/Public/Videos` | `CommonVideos` |
| `C:/Program Files` | `ProgramFiles` |
| `C:/Program Files/Common Files` | `CommonProgramFiles` |
| `C:/ProgramData` | `CommonApplicationData` |
| `C:/ProgramData/Microsoft/Windows/Start Menu` | `CommonStartMenu` |
| `C:/ProgramData/Microsoft/Windows/Start Menu/Programs` | `CommonPrograms` |
| `C:/ProgramData/Microsoft/Windows/Start Menu/Programs/Startup` | `CommonStartup` |
| `C:/WINDOWS/` | `Windows` |
| `C:/WINDOWS/system32` | `System` |
| `C:/WINDOWS/fonts` | `Fonts` |
