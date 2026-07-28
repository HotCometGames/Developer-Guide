# Game Engines

> Deep dive into Unity, Godot, Unreal Engine, and raw frameworks — features, trade-offs, and how to choose.

---

## What Is It?

A game engine is a framework that handles the low-level plumbing of game development: rendering, physics, audio, input, and asset management. Instead of writing a renderer from scratch, you use the engine's tools and focus on making the game.

> **Related:** [What Is Game Dev?](what-is-gamedev.md) for the mental model. [Game Loop](game-loop.md) for how engines run your code.

---

## Why Use an Engine?

| Without Engine | With Engine |
|----------------|-------------|
| Write your own renderer | Built-in rendering pipeline |
| Write your own physics | Built-in physics engine |
| Write your own input system | Built-in input handling |
| Write your own audio | Built-in audio system |
| Months/years of setup | Start building immediately |

**When to skip the engine:** You want to learn how engines work, your game is very simple (Pong, Tetris), or you have very specific requirements.

## Engine Comparison

| Feature | Unity | Godot | Unreal | Pygame/Raylib |
|---------|-------|-------|--------|---------------|
| **Language** | C# | GDScript, C# | C++, Blueprints | C, C++, Python |
| **2D Support** | Good | Excellent | Basic | Excellent |
| **3D Support** | Good | Good | Excellent | Basic |
| **Cost** | Free tier + revenue share | Free, open-source | Free + royalty after $1M | Free, open-source |
| **Learning Curve** | Medium | Low | High | Low-Medium |
| **Platform Support** | All major + web | PC, mobile, web | PC, console | PC, mobile |
| **Asset Store** | Large marketplace | Growing library | Marketplace | N/A |
| **Community** | Largest | Growing fast | Large | Small-medium |
| **Best For** | Cross-platform, mobile | 2D, indie, learning | AAA 3D, high fidelity | Learning, simple games |

## Unity

### What It Is

Unity is the most widely used game engine, especially for indie and mobile games. It uses C# for scripting and has a visual editor for scene building.

### Strengths

| Strength | Why It Matters |
|----------|---------------|
| Cross-platform | Build once, deploy to 20+ platforms |
| Large community | Answers to every question |
| Asset Store | Ready-made art, tools, plugins |
| C# scripting | Familiar language for .NET developers |
| Mature tooling | Profiler, debugger, editor tools |

### Weaknesses

| Weakness | Impact |
|----------|--------|
| Runtime fee controversy | Pricing changes can affect projects |
| Not open-source | Can't modify the engine itself |
| 3D not as strong as Unreal | AAA quality requires more work |
| GC pauses | Garbage collection can cause hitches |

### Key Concepts

| Concept | What It Is |
|---------|-----------|
| GameObject | Any object in the scene |
| Component | Behavior/data attached to GameObject |
| MonoBehaviour | Base class for custom scripts |
| ScriptableObject | Data container for configuration |
| Prefab | Reusable GameObject template |
| Scene | Collection of GameObjects |
| Unity Editor | Visual tool for building games |

### C# Script Example

```csharp
using UnityEngine;

public class PlayerController : MonoBehaviour
{
    [SerializeField] private float speed = 5f;
    [SerializeField] private float jumpForce = 10f;
    
    private Rigidbody2D rb;
    private bool isGrounded;

    void Start()
    {
        rb = GetComponent<Rigidbody2D>();
    }

    void Update()
    {
        float horizontal = Input.GetAxis("Horizontal");
        transform.position += Vector3.right * horizontal * speed * Time.deltaTime;

        if (Input.GetButtonDown("Jump") && isGrounded)
        {
            rb.AddForce(Vector2.up * jumpForce, ForceMode2D.Impulse);
        }
    }

    void OnCollisionEnter2D(Collision2D col)
    {
        if (col.gameObject.CompareTag("Ground"))
            isGrounded = true;
    }

    void OnCollisionExit2D(Collision2D col)
    {
        if (col.gameObject.CompareTag("Ground"))
            isGrounded = false;
    }
}
```

## Godot

### What It Is

Godot is a free, open-source game engine with a focus on 2D and rapid iteration. It uses GDScript (Python-like) or C# for scripting and has a unique node-based scene system.

### Strengths

| Strength | Why It Matters |
|----------|---------------|
| Free and open-source | No fees, full source access |
| Excellent 2D tools | Best-in-class 2D workflow |
| GDScript | Easy to learn, Python-like |
| Fast iteration | Quick code→test cycle |
| Lightweight | Runs on modest hardware |
| Growing rapidly | Active development, community |

### Weaknesses

| Weakness | Impact |
|----------|--------|
| Smaller community | Fewer tutorials and assets |
| 3D less mature | Not ideal for AAA 3D |
| Fewer platforms | No console export in free tier |
| GDScript is niche | Skills don't transfer directly |

### Key Concepts

| Concept | What It Is |
|---------|-----------|
| Node | Any object in the scene tree |
| Scene | Reusable collection of nodes |
| Signal | Event system for communication |
| GDScript | Python-like scripting language |
| Export | Variable visible in editor |
| @onready | Initialize variable when node is ready |

### GDScript Example

```gdscript
extends CharacterBody2D

@export var speed: float = 200.0
@export var jump_force: float = -400.0

var gravity = ProjectSettings.get_setting("physics/2d/default_gravity")

func _physics_process(delta):
    velocity.y += gravity * delta

    if Input.is_action_just_pressed("jump") and is_on_floor():
        velocity.y = jump_force

    var direction = Input.get_axis("left", "right")
    velocity.x = direction * speed

    move_and_slide()

func _on_area_entered(area):
    if area.is_in_group("coin"):
        area.queue_free()
        print("Coin collected!")
```

## Unreal Engine

### What It Is

Unreal Engine is Epic Games' AAA game engine, known for high-fidelity 3D graphics. It uses C++ and Blueprints (visual scripting) for game logic.

### Strengths

| Strength | Why It Matters |
|----------|---------------|
| Best-in-class 3D | Photorealistic graphics possible |
| Blueprints | Visual scripting for non-coders |
| Massive marketplace | High-quality assets and plugins |
| Industry standard | Used in AAA studios |
| Nanite/Lumen | Cutting-edge rendering tech |

### Weaknesses | Weakness | Impact |
|----------|--------|
| Heavy | Requires powerful hardware |
| Steep learning curve | Complex for beginners |
| C++ complexity | Harder than C# or GDScript |
| Overkill for 2D | Poor 2D tooling |
| Large build sizes | Not ideal for mobile/web |

### Blueprints vs C++

| Approach | When to Use |
|----------|-------------|
| Blueprints | Prototyping, designers, simple logic |
| C++ | Performance-critical, complex systems |
| Both | Blueprint for iteration, C++ for core |

## Raw Frameworks

### When to Use

| Use Case | Framework |
|----------|-----------|
| Learning game dev fundamentals | Pygame, Raylib, Love2D |
| Very simple games | Any lightweight framework |
| Custom engine needs | Raylib, SFML, SDL2 |
| Maximum control | Raw OpenGL/Vulkan |

### Popular Frameworks

| Framework | Language | Best For |
|-----------|----------|----------|
| Pygame | Python | Learning, prototyping |
| Raylib | C | Learning, simple games |
| Love2D | Lua | 2D games, game jams |
| MonoGame | C# | XNA-style games |
| SFML | C++ | Multimedia, 2D |
| SDL2 | C | Low-level, cross-platform |

## How to Choose

### Decision Factors

| Factor | Unity | Godot | Unreal | Framework |
|--------|-------|-------|--------|-----------|
| Your experience | Intermediate | Beginner | Advanced | Any |
| 2D game | Good | Best | Poor | Excellent |
| 3D game | Good | Good | Best | Manual |
| Mobile target | Best | Good | Okay | Manual |
| Team size | Any | Solo/small | Large | Solo |
| Budget | Free tier | Free | Free + royalty | Free |
| Learning goal | Industry skills | Rapid prototyping | AAA quality | Fundamentals |

### The Recommendation

> **Start with Godot** if you're new to game dev. It's free, lightweight, has excellent 2D tools, and GDScript is easy to learn. You can always move to Unity or Unreal later.

## Best Practices

- **Learn one engine well** — Don't bounce between engines
- **Use the engine's patterns** — Don't fight the architecture
- **Build in the editor** — Use visual tools, not just code
- **Version control your project** — Git works for game dev
- **Test on target hardware** — Performance varies by device
- **Read the engine's docs** — Official docs are usually best

## Common Mistakes

| Mistake | Problem | Solution |
|---------|---------|----------|
| Choosing engine by popularity | Wrong tool for your game | Choose by requirements |
| Fighting the engine | Reinventing the wheel | Learn and use engine patterns |
| Not using the editor | Missing built-in tools | Use visual tools |
| Ignoring performance | Frame drops in production | Profile early and often |
| Not backing up | Lost work | Git init first, commit often |

## Related Topics

- [Game Loop](game-loop.md) — How engines run your code
- [ECS](ecs.md) — Architecture pattern used by modern engines
- [Performance](performance.md) — Optimization within your engine

## Further Learning

- [Unity Manual](https://docs.unity3d.com/Manual/) — Official Unity docs
- [Godot Docs](https://docs.godotengine.org/) — Official Godot docs
- [Unreal Docs](https://docs.unrealengine.com/) — Official Unreal docs
- [Raylib Examples](https://www.raylib.com/examples.html) — C framework examples

---

## Personal Notes

> Add your own notes, reminders, and experiences here.
