# Unity Editor

> Unity's visual editor for building 2D and 3D games: scene editing, asset management, and core workflows.

> **Related:** [Godot](godot.md) | [Unreal Engine](unreal-engine.md) | [AI Coding Tools](ai-coding-tools.md)

---

## What Is It?

The Unity Editor is the primary interface for creating games in Unity. It combines a scene view, asset pipeline, animation tools, lighting system, and inspector into one environment. C# scripts control game behavior; the editor handles the visual and structural layers.

## Editor Layout

| Panel | Purpose |
|-------|---------|
| **Scene View** | Visual 3D/2D world editor — select, move, rotate, scale objects |
| **Game View** | What the player will see — run and test your game |
| **Hierarchy** | List of all objects in the current scene |
| **Inspector** | Properties of the selected object (components, transforms, materials) |
| **Project** | File browser for all assets in the project |
| **Console** | Logs, warnings, and errors |
| **Toolbar** | Play, pause, step buttons; transform tools; layers |
| **Animation** | Timeline, curves, keyframes for animating objects |

### Layout Presets

Save custom layouts via **Window → Layouts → Save Layout**. Common layouts:

- **Default** — balanced for general use
- **2D** — larger Scene View, minimized 3D tools
- **Animation** — expanded Animation and Animator windows
- **Debug** — Console, Profiler, and Frame Debugger visible

## Core Workflows

### Scene Building

1. Create objects in the Hierarchy (or drag models from the Project window)
2. Position, rotate, and scale with the transform tools (Q, W, E, R, T, Y)
3. Add components via the Inspector — colliders, rigidbodies, scripts, audio sources
4. Apply materials and shaders for visual appearance

### Prefabs

Prefabs are reusable object templates. Changes to a prefab asset update all instances.

| Action | How |
|--------|-----|
| Create prefab | Drag an object from Hierarchy to Project window |
| Edit prefab | Double-click the prefab in Project or click the arrow next to its name in Hierarchy |
| Override property | Change a value on an instance — bold text indicates an override |
| Apply overrides | Right-click the property → Apply to Prefab |
| Revert | Right-click → Revert |

### Materials & Shaders

- **Materials** define surface properties (color, texture, roughness, metalness)
- **Shaders** are programs that calculate pixel appearance
- Use the **Standard Shader** for most PBR materials
- **Shader Graph** provides node-based shader creation

### Lighting

| Type | What It Does |
|------|-------------|
| Directional Light | Sun — affects everything |
| Point Light | Local light source (like a bulb) |
| Spot Light | Cone-shaped light |
| Area Light | Rectangle light source (baked only) |
| Ambient Light | Global fill light from the sky/environment |

### Audio

| Component | Purpose |
|-----------|---------|
| Audio Source | Emits sound from a GameObject |
| Audio Listener | "Ear" — attached to the camera by default |
| Audio Mixer | Group, route, and apply effects to audio |

## Scripting

Unity scripts are C# classes that inherit from `MonoBehaviour`:

```csharp
using UnityEngine;

public class PlayerController : MonoBehaviour
{
    public float speed = 5f;

    void Update()
    {
        float move = Input.GetAxis("Horizontal") * speed * Time.deltaTime;
        transform.Translate(move, 0, 0);
    }
}
```

| Lifecycle Method | When It Runs |
|-----------------|-------------|
| `Awake()` | When the object is loaded (before Start) |
| `Start()` | Before the first frame update |
| `Update()` | Every frame |
| `FixedUpdate()` | Every physics step (fixed timestep) |
| `LateUpdate()` | After all Update calls |
| `OnCollisionEnter()` | When a collision starts |

## Build Pipeline

1. Open **File → Build Profiles** (or **File → Build Settings** in older versions)
2. Select the target platform
3. Add the scenes to include
4. Configure player settings (icon, name, resolution)
5. Click **Build**

### Supported Platforms

| Platform | Notes |
|----------|-------|
| Windows, macOS, Linux | Desktop builds |
| iOS, Android | Mobile builds |
| WebGL | Browser builds |
| PlayStation, Xbox, Switch | Console (requires platform license) |

## Performance Tools

| Tool | What It Does |
|------|-------------|
| **Profiler** | CPU, GPU, memory, rendering — per-frame breakdown |
| **Frame Debugger** | Step through each draw call |
| **Memory Profiler** | Detailed memory snapshot analysis |
| **Statistics** | View toggle — shows FPS, draw calls, triangles |

## What's Next?

Compare the Unity Editor workflow with [Godot](godot.md) or [Unreal Engine](unreal-engine.md).
