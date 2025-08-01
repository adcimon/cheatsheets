# Visual Studio

<p align="center"><img align="center" width="20%" height="20%" src="assets/visualstudio.svg"></p>

[Visual Studio](https://en.wikipedia.org/wiki/Microsoft_Visual_Studio) is an integrated development environment (IDE) from Microsoft.

## Index

* [General](#general)
* [Editor](#editor)
* [C/C++](#cc)
* [Build](#build)
* [Debug](#debug)

## General

Add manifest file.
* Right click on `Solution Explorer → Project → Add → New Item → Application Manifest File`.
* The file `app.manifest` will be created.

## Editor

Fix inconsistent line endings.
* Go to `Edit → Find and Replace → Quick Replace`.
* Check `Use Regular Expressions`.
* Replace `(?<!\r)\n` for `\r\n`.

Hide reference counts.
* Go to `Tools → Options → Text Editor → All Languages → CodeLens`.
* Uncheck `Enable CodeLens` or `Show C# and Visual Basic References`.

Hide vertical dotted indentation.
* Go to `Tools → Options → Text Editor`.
* Uncheck `Show structure guide lines`.

## C/C++

Add include directories.
* Go to `Project → Properties → C/C++ → General`.
* Add to `Additional Include Directories` the path `$(ProjectDir)path\to\include`.

Add library directories.
* Go to `Project → Properties → Linker → General`.
* Add to `Additional Library Directories` the path `$(ProjectDir)path\to\lib`.

Add library.
* Go to `Project → Properties → Linker → Input`.
* Add to `Additional Dependencies` the `.lib` file.

## Build

Change build directory.
* Go to `Project → Properties → General`.
* Change `Output Directory` to `$(SolutionDir)build\$(Platform)\$(Configuration)\`.
* Change `Intermediate Directory` to `$(SolutionDir)build\intermediate\$(Platform)\$(Configuration)\`.

Copy files on post-build.
* Go to `Project → Properties → Build Events → Post-Build Event`.
* Add to `Command line` the instruction `copy /Y $(ProjectDir)path\to\files\*.ext $(OutDir)`.

## Debug

Automatically close console when debug stops.
* Go to `Tools → Options → Debugging`.
* Check `Automatically close the console when debugging stops`.

Run debug as administrator.
* Go to `app.manifest` → `<requestedPrivileges>` and add the execution level requirement:
```
<requestedExecutionLevel level="requireAdministrator" uiAccess="false"/>
```
* When trying to debug, the editor will warn about the admin right and restart itself with admin rights.
* The executable will be marked as requiring admin rights, therefore when deploying is not necessary to configure admin rights in the file properties.
