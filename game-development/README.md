# Game Development

## Index

* [Networking](#networking)
* [Unity Conventions](#unity-conventions)
  * [Directory Structure](#directory-structure)
  * [Asset Naming](#asset-naming)
  * [Code Style](#code-style)

## Networking

* [Fast-Paced Multiplayer](https://www.gabrielgambetta.com/client-server-game-architecture.html)
* [Game Networking Demystified](https://ruoyusun.com/2019/03/28/game-networking-1.html)
* [How do Video Games Stay in Sync](https://medium.com/geekculture/how-do-video-games-stay-in-sync-an-intro-to-the-fascinating-networking-of-real-time-games-e923e66e8a0f)

Case Studies
* [1500 Archers on a 28.8: Network Programming in Age of Empires and Beyond](https://www.gamedeveloper.com/programming/1500-archers-on-a-28-8-network-programming-in-age-of-empires-and-beyond)
* [Overwatch Gameplay Architecture and Netcode](https://www.youtube.com/watch?v=W3aieHjyNvw)
* [Factorio - The multiplayer megapacket](https://factorio.com/blog/post/fff-302)

## Unity Conventions

### Directory Structure

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

### Asset Naming

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

### Code Style

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
