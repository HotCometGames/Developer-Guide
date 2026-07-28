# Unreal Engine

> Unreal Editor's workflow: Blueprints, C++, level design, and high-fidelity rendering.

> **Related:** [Unity Editor](unity-editor.md) | [Godot](godot.md)

---

## What Is It?

Unreal Engine is a game engine developed by Epic Games, known for high-fidelity graphics, a node-based scripting system (Blueprints), and full C++ access. The Unreal Editor is the interface for building levels, scripting behavior, and compiling games.

## Editor Layout

| Panel | Purpose |
|-------|---------|
| **Viewport** | 3D level view — navigate with WASD, right-click to look |
| **Content Browser** | Asset library — models, textures, materials, Blueprints |
| **World Outliner** | List of all actors in the current level |
| **Details** | Properties of the selected actor |
| **Place Actors** | Palette of spawnable actors |
| **Unreal Editor Toolbar** | Play, simulate, and build controls |
| **Modes** | Place, Paint, Landscape, Foliage, Geometry Edit |

## Blueprints

Blueprints are Unreal's visual scripting system. Instead of writing code, you connect nodes in a graph.

### Blueprint Types

| Type | Purpose |
|------|---------|
| **Level Blueprint** | Level-specific logic (doors, triggers, win conditions) |
| **Blueprint Class** | Reusable actor class (enemy, pickup, weapon) |
| **Blueprint Interface** | Shared method signatures across Blueprints |
| **Widget Blueprint** | UI screens and HUD elements |

### Blueprint vs C++

| Aspect | Blueprints | C++ |
|--------|-----------|-----|
| Speed to prototype | Fast | Slow |
| Runtime performance | Slower | Fast |
| Visual debugging | Excellent | Requires tooling |
| Complex logic | Becomes messy spaghetti | Cleaner for complex systems |
| Team suited for | Designers, artists | Engineers |

**Typical workflow:** Prototype in Blueprints, profile to find hotspots, rewrite performance-critical code in C++.

## C++ in Unreal

Unreal C++ extends standard C++ with a reflection system:

```cpp
UCLASS()
class AMyActor : public AActor
{
    GENERATED_BODY()

public:
    UPROPERTY(EditAnywhere, BlueprintReadWrite)
    float Health = 100.0f;

    UFUNCTION(BlueprintCallable)
    void TakeDamage(float DamageAmount);
};
```

| Macro | Purpose |
|-------|---------|
| `UCLASS()` | Marks a class for Unreal's reflection system |
| `UPROPERTY()` | Exposes a variable to the editor and Blueprints |
| `UFUNCTION()` | Makes a function callable from Blueprints |
| `GENERATED_BODY()` | Required boilerplate in every UCLASS |

## Level Building

| Tool | What It Does |
|------|-------------|
| **Geometry Brush** | Create BSP brushes for prototyping levels |
| **Landscape** | Sculpt terrain with heightmaps and layers |
| **Foliage** | Paint grass, trees, rocks on terrain |
| **Modeling Mode** | Mesh editing, boolean operations, polygonal modeling |

## Materials

Unreal's material system is node-based and highly flexible. Materials define how surfaces react to light:

- **Base Color** — surface color/albedo
- **Metallic** — how metallic the surface is
- **Roughness** — how rough or smooth the surface is
- **Normal** — surface detail via normal maps
- **Emissive** — self-illumination
- **Opacity** — transparency mask

## Lighting

| Light Type | Behavior |
|------------|----------|
| Directional Light | Sun (parallel rays, affects everything) |
| Point Light | Omni-directional from a point |
| Spot Light | Cone-shaped beam |
| Rect Light | Rectangle area light (soft shadows) |
| Sky Light | Captures distant environment lighting |
| Sky Atmosphere | Dynamic sky rendering (atmospheric scattering) |

**Lighting modes:** Baked (pre-computed, static), Stationary (mixed), Movable (dynamic, expensive).

## Performance Tools

| Tool | What It Does |
|------|-------------|
| **GPU Visualizer** | Per-draw call GPU cost breakdown |
| **Stat Commands** | `stat fps`, `stat unit`, `stat game` — runtime stats |
| **ProfileGPU** | Captures GPU frame data |
| **Unreal Insights** | Deep performance tracing and analysis |

## Exporting & Platforms

1. Open **File → Package Project**
2. Select target platform
3. Configure project settings
4. Click **Package**

Unreal supports Windows, macOS, Linux, iOS, Android, PlayStation, Xbox, and Switch.

## Best Practices

- **Blueprint first, C++ second** — iterate fast, optimize later
- **Use level streaming** — split large worlds into loadable chunks
- **Optimize draw calls** — merge static meshes, use instancing
- **Control asset quality** — use LODs, texture atlases, and mipmaps
- **Leverage the Marketplace** — many free assets and systems available
