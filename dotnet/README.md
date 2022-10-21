# .NET

<p align="center"><img align="center" width="20%" height="20%" src="assets/dotnet.svg"></p>

[.NET](https://en.wikipedia.org/wiki/.NET) is a free and open-source, managed computer software framework for Windows, Linux, and macOS operating systems. The project is primarily developed by Microsoft employees by way of the [.NET Foundation](https://en.wikipedia.org/wiki/.NET_Foundation), and released under the MIT License.

## Index

* [Dotnet](#dotnet)
  * [Publish](#publish)
* [Special Folders](#special-folders)

## Dotnet

The command-line interface (CLI) [dotnet](https://learn.microsoft.com/en-us/dotnet/core/tools/) is a cross-platform toolchain for developing, building, running, and publishing .NET applications.

### Publish

The [dotnet publish](https://learn.microsoft.com/en-us/dotnet/core/tools/dotnet-publish) command publishes the application and its dependencies to a folder for deployment to a hosting system.

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
