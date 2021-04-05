## Table of Contents

* [Directory Structure](#directory-structure)
* [Asset Naming](#asset-naming)
* [Code Style](#code-style)

## Directory Structure

Prototype.
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

Project.
```
Assets
├── Animations
├── Audio
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
| Atlas | <Name>.atlas |
| Animation | [<ModelName>@]<Name>.anim |
| Animator Controller | <Name> |
| Avatar Mask | <Name> |
| Material | <Name> |
| Mesh | <Name> |
| Model | <Name> |
| Music | <Name>.music |
| Prefab | <Name> |
| Sound Effect | <Name>.sfx |
| Sprite | <Name>.sprite |
| Texture | <Name>.<TextureType> |
| Visual Effect | <Name>.vfx |
| Video | <Name> |

| Texture Type | Code |
| - | - |
| Albedo | albedo |
| Ambient Occlusion | occlusion |
| Anisotropic Filter | aniso |
| Diffuse | diffuse |
| Displacement | displacement |
| Distance Field | distancefield |
| Emissive | emissive |
| Flow | flow |
| Height | height |
| Icon | icon |
| Light | light |
| Mask | mask |
| Metallic | metallic |
| Normal | normal |
| Roughness | roughness |
| Screen Space Scattering | sss |
| Specular | specular |
| Tile | tile |
| Vector Field | vectorfield |

## Code Style
