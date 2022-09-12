# Unity Conventions

## Index

* [Directory Structure](#directory-structure)
* [Asset Naming](#asset-naming)
* [Code Style](#code-style)

## Directory Structure

Prototype
```
Assets
├── Animations
├── Audio
│   ├── Music
│   └── Sound
├── Fonts
├── Materials
├── Models
├── Prefabs
├── Scenes
├── Scripts
├── Shaders
├── Sprites
├── Textures
├── VFX
└── Video
```

Project
```
Assets
├── Animations
├── Audio
│   ├── Music
│   └── Sound
├── Code
│   ├── Core
│   ├── Editor
│   ├── Game
│   ├── Shader
│   └── Test
├── Fonts
├── Materials
├── Models
├── Prefabs
├── Scenes
├── Sprites
├── Textures
├── VFX
└── Video
```

Despite the separation of the assets by type, if an asset is compossed of multiple subassets, these should be included in the corresponding subfolder.
```
Models
├── ...
├── Orc
│   ├── Orc.fbx
│   ├── Animations
│   │   ├── Orc@Attack.fbx
│   │   ├── Orc@Attack.anim
│   │   └── Orc.controller
│   ├── Materials
│   │   └── Orc.mat
│   └── Textures
│       └── Orc.diffuse.png
└── ...
```

## Asset Naming

| Asset Type | Asset Name |
| - | - |
| Atlas | \<Name\>.atlas |
| Animation | [\<ModelName\>@]\<Name\> |
| Animator Controller | \<ModelName\>Controller |
| Avatar Mask | \<Name\>Mask |
| Material | \<Name\> |
| Mesh | \<Name\> |
| Model | \<Name\> |
| Music | \<Name\>.music |
| Prefab | \<Name\> |
| Sound Effect | \<Name\>.sfx |
| Sprite | \<Name\>.sprite |
| Texture | \<Name\>.\<TextureType\> |
| Visual Effect | \<Name\>.vfx |
| Video | \<Name\> |

| Texture Type | Code |
| - | - |
| Albedo | alb |
| Ambient Occlusion | occ |
| Anisotropic Filter | ani |
| Diffuse | diff |
| Displacement | disp |
| Distance Field | df |
| Emissive | emi |
| Flow | flow |
| Gradient | grad |
| Height | height |
| Icon | ico |
| Light | light |
| Mask | mask |
| Metallic | met |
| Normal | norm |
| Roughness | roug |
| Subsurface Scattering | sss |
| Specular | spec |
| Tile | tile |
| Vector Field | vf |
| Vertex Animation Texture | vat |

## Code Style

| Language Concept | Convention |
| - | - |
| Namespace | PascalCasing |
| Generic Type | T |
| Struct | PascalCasing |
| Class | PascalCasing |
| Interface | IPascalCasing |
| Enum | PascalCasing |
| Method | PascalCasing |
| Attribute | camelCasing |
| Property | camelCasing |
| Parameter | camelCasing |
| Unary operator overload parameter | value |
| Binary operator overload parameter | left, right |

### References

* [Create a C# style guide: Write cleaner code that scales](https://resources.unity.com/games/create-code-style-guide-e-book)
* [Clean up your code: How to create your own C# code style](https://blog.unity.com/technology/clean-up-your-code-how-to-create-your-own-c-code-style)
* [.NET Framework Design Guidelines](https://docs.microsoft.com/en-us/dotnet/standard/design-guidelines/)
* [C# Coding Conventions](https://docs.microsoft.com/en-us/dotnet/csharp/fundamentals/coding-style/coding-conventions)
* [C# at Google Style Guide](https://google.github.io/styleguide/csharp-style.html)
* [Unity C# Code Style Guide Example](https://github.com/thomasjacobsen-unity/Unity-Code-Style-Guide)
