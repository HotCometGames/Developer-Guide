# Godot

> Godot's open-source editor: scene system, node-based architecture, and GDScript.

> **Related:** [Unity Editor](unity-editor.md) | [Unreal Engine](unreal-engine.md)

---

## What Is It?

Godot is a free, open-source game engine with a fully integrated editor. Unlike Unity and Unreal, the Godot editor itself is built with Godot's own UI system. It's lightweight, starts fast, and is designed around a node-scene architecture.

## Editor Layout

| Panel | Purpose |
|-------|---------|
| **Viewport** | The 2D/3D scene canvas |
| **Scene** | Tree of nodes in the current scene |
| **Inspector** | Properties of the selected node |
| **FileSystem** | Project file browser |
| **Output** | Debug output |
| **Bottom Panel** | Audio, animation, debugger, remote inspector |

## Node-Scene Architecture

Everything in Godot is a **node**. Nodes are organized in a tree. A **scene** is a tree of nodes saved as a `.tscn` file.

```
Player (CharacterBody2D)
├── Sprite2D
├── CollisionShape2D
└── AudioStreamPlayer2D
```

Scenes can be instanced inside other scenes — like Unity prefabs but more fundamental. The entire game is a tree of nodes.

## Scripting

Godot supports three languages:

| Language | Best For | Notes |
|----------|----------|-------|
| **GDScript** | Most gameplay | Python-like, designed for Godot, tight editor integration |
| **C#** | Performance-heavy logic | Full .NET support, familiar to Unity developers |
| **VisualScript** | Non-programmers | Node-based visual programming (legacy, less maintained) |

### GDScript Example

```gdscript
extends CharacterBody2D

@export var speed := 300.0

func _physics_process(delta: float) -> void:
    var direction := Input.get_axis("move_left", "move_right")
    velocity.x = direction * speed
    move_and_slide()
```

Lifecycle methods follow Godot's naming convention with underscores.

## Signals

Signals are Godot's event system — nodes emit signals, other nodes connect to them:

```gdscript
# In a button node script
signal button_pressed

func _on_pressed() -> void:
    button_pressed.emit()

# Connect in another node
$Button.button_pressed.connect(_on_button_action)
```

Connections can be made in the editor visually or in code.

## Scene System vs Unity

| Godot | Unity |
|-------|-------|
| .tscn files (text-based, human-readable) | .unity scenes (binary/YAML) |
| Every node is part of a scene | GameObjects live in scenes |
| Scenes nest freely | Prefabs are special |
| Built-in animation player | Animator + Animation windows |
| Own scripting language (GDScript) + C# | C# only |

## Key Differences

- **Size** — Godot editor is ~50MB; Unity is ~3GB
- **License** — MIT (no royalties, no seat licenses)
- **2D** — Godot's 2D engine is a strong point; dedicated 2D renderer (not 3D-on-a-plane)
- **3D** — Improving but behind Unity/Unreal in features and performance
- **Export** — Lightweight export templates per platform

## Exporting

1. Open **Project → Export**
2. Install export templates for your target platform
3. Configure presets for each platform
4. Click **Export Project**

## Best Practices

- **Use scenes for everything** — even a single bullet should be its own scene
- **Prefer GDScript for gameplay** — it's what Godot is optimized for
- **Use signals** — they keep your code decoupled
- **Export variables** (`@export`) — tweak values in the inspector without re-opening the script
- **Keep node trees shallow** — deep nesting is harder to navigate
