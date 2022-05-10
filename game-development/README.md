# Game Development

## Index

* [Animation](#animation)
* [Procedural Generation](#procedural-generation)
* [Networking](#networking)
* [Unity Conventions](#unity-conventions)
  * [Directory Structure](#directory-structure)
  * [Asset Naming](#asset-naming)
  * [Code Style](#code-style)

## Animation

* [Animation Instancing - Instancing for SkinnedMeshRenderer](https://blog.unity.com/technology/animation-instancing-instancing-for-skinnedmeshrenderer)
* [Texture Animation: Applying Morphing and Vertex Animation Techniques](https://medium.com/tech-at-wildlife-studios/texture-animation-techniques-1daecb316657)
* [How To Render 10,000 Animated Characters With 20 Draw Calls In Unity](https://medium.com/chenjd-xyz/how-to-render-10-000-animated-characters-with-20-draw-calls-in-unity-e30a3036349a)
* [Dev Diary — Skeletal Animation and GPU Skinning](https://yadiyasheng.medium.com/skeletal-animation-and-gpu-skinning-c99b30eb2ca2)

## Procedural Generation

Wave Function Collapse
* [Infinite procedurally generated city with the Wave Function Collapse algorithm](https://marian42.de/article/wfc/)
* [Wave Function Collapse - Procedural Building Generation in Unity](https://www.uproomgames.com/dev-log/wave-function-collapse)
* [The Wavefunction Collapse Algorithm explained very clearly](https://robertheaton.com/2018/12/17/wavefunction-collapse-algorithm/)

## Networking

* [Fast-Paced Multiplayer](https://www.gabrielgambetta.com/client-server-game-architecture.html)
* [Game Networking Demystified](https://ruoyusun.com/2019/03/28/game-networking-1.html)

Case Studies
* [1500 Archers on a 28.8: Network Programming in Age of Empires and Beyond](https://www.gamedeveloper.com/programming/1500-archers-on-a-28-8-network-programming-in-age-of-empires-and-beyond)
* [Overwatch Gameplay Architecture and Netcode](https://www.youtube.com/watch?v=W3aieHjyNvw)
* [Factorio - The multiplayer megapacket](https://factorio.com/blog/post/fff-302)

## Unity Conventions

### Directory Structure

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