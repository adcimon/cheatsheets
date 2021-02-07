# Unity

[Unity](https://unity.com/) is a cross-platform game engine.

## Packages
A package is a container that holds any combination of Assets, Shaders, Textures, plug-ins, icons, and scripts that enhance various parts of the project.

Package manifests, `package.json` files, determine which version of the package to load, and what information to display in the Package Manager.
```
{
    "name": "com.adcimon.mypackage",
    "displayName": "My Package",
    "version": "0.0.1",
    "type": "library",
    "unity": "2019.3",
    "description": "My awesome package",
    "keywords": [
        "gui",
        "maths"
    ],
    "category": "Interface",
    "dependencies": {
        "com.unity.ugui": "1.0.0"
    }
}
```
* `name` is the officially registered package name, following the naming convention `com.[org].[name]`.
* `displayName` is the package name as it appears in the Package Manager.
* `version` is the package version following the [Semantic Versioning](https://semver.org/) system `MAJOR.MINOR.PATCH`.
* `type` specifies the type of the package, `tests`, `sample`, `template`, `module`, `library` or `tool`.
* `unity` is the Unity version that supports the package.
* `description` is a brief description of the package.
* `keywords` are used for searching in the Package Manager, specified as a JSON array of strings.
* `category` specifies the category the packages is in.
* `dependencies` is a list of packages that the package depends on, expressed as a JSON dictionary where the key is the package name and the value is the version number. Unity downloads all dependencies and loads them into the project alongside the package.
