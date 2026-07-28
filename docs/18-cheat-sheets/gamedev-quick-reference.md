# Game Development Quick Reference

> One-page reference for game engines, game loop, ECS, physics, and input handling. Print this or bookmark it.

---

## Game Loop

```
while game is running:
    process input
    update game state
    render frame
```

### Fixed vs Variable Timestep

| Approach | Pros | Cons |
|----------|------|------|
| Fixed | Deterministic, physics-friendly | May skip frames or lag |
| Variable | Smooth on all hardware | Non-deterministic physics |
| Semi-fixed | Best of both | More complex |

## Unity Quick Reference

### Essential Shortcuts

| Shortcut | Action |
|----------|--------|
| `F` | Focus on selected object |
| `W/E/R` | Move/Rotate/Scale tools |
| `Ctrl+Shift+F` | Align view to object |
| `Ctrl+P` | Play/Pause |
| `Ctrl+Shift+P` | Step |
| `Ctrl+D` | Duplicate |
| `Ctrl+Z` | Undo |
| `Ctrl+S` | Save scene |
| `Space` | Toggle play mode |

### Common C# Patterns

```csharp
// MonoBehaviour lifecycle
void Awake() { }       // Called once when created
void Start() { }       // Called before first frame
void Update() { }      // Called every frame
void FixedUpdate() { }  // Called at fixed intervals
void LateUpdate() { }  // Called after all Updates

// Movement
transform.Translate(Vector3.forward * speed * Time.deltaTime);
transform.position += direction * speed * Time.deltaTime;

// Input
if (Input.GetKeyDown(KeyCode.Space)) { }
if (Input.GetButtonDown("Jump")) { }
float h = Input.GetAxis("Horizontal");

// Instantiate prefab
Instantiate(prefab, position, rotation);

// Destroy object
Destroy(gameObject, 2f); // after 2 seconds
```

### Physics

| Component | Purpose |
|-----------|---------|
| Rigidbody | Enables physics simulation |
| Collider | Defines collision shape |
| Trigger Collider | Detects overlap, no physics |
| Joint | Connects rigidbodies |

```csharp
// Apply force
GetComponent<Rigidbody>().AddForce(Vector3.up * force);

// Check collision
void OnCollisionEnter(Collision col) { }
void OnTriggerEnter(Collider other) { }
```

## Godot Quick Reference

### Essential Shortcuts

| Shortcut | Action |
|----------|--------|
| `F5` | Run project |
| `F6` | Run current scene |
| `F8` | Stop |
| `Ctrl+Shift+S` | Save scene |
| `Ctrl+S` | Save all |
| `Ctrl+A` | Add node |
| `Ctrl+D` | Duplicate |
| `W/E/R` | Move/Rotate/Scale |

### GDScript Basics

```gdscript
# Node references
@onready var sprite = $Sprite2D
@onready var label = $Label

# Lifecycle
func _ready():        # Called when node enters tree
func _process(delta): # Called every frame
func _physics_process(delta): # Called at fixed rate

# Movement
position += velocity * delta
velocity = Input.get_vector("left", "right", "up", "down") * speed

# Signals
signal health_changed(new_health)
emit_signal("health_changed", health)
func _on_health_changed(new_health): pass

# Input
if Input.is_action_just_pressed("jump"):
    velocity.y = jump_force
```

## Unreal Engine Quick Reference

### Essential Shortcuts

| Shortcut | Action |
|----------|--------|
| `W/E/R` | Move/Rotate/Scale |
| `F` | Focus on selection |
| `Ctrl+L` | Toggle light |
| `Ctrl+G` | Group actors |
| `Alt+Drag` | Duplicate |
| `Ctrl+Shift+S` | Save current |
| `Esc` | Deselect |

### Blueprint Concepts

| Concept | Description |
|---------|-------------|
| Event Graph | Where logic lives |
| Construction Script | Runs in editor |
| Components | Modular functionality |
| Variables | Stored data |
| Functions | Reusable logic blocks |
| Macros | Inline code blocks |

## ECS (Entity Component System)

| Concept | Description | Example |
|---------|-------------|---------|
| Entity | Just an ID | Player, Enemy, Bullet |
| Component | Data only | Position, Health, Sprite |
| System | Logic only | MovementSystem, RenderSystem |

### Benefits

| Benefit | Why |
|---------|-----|
| Data-oriented | Cache-friendly, fast |
| Composition over inheritance | Flexible, no deep hierarchies |
| Separation of concerns | Clean, testable code |
| Easy to add features | Just add components and systems |

## 2D Math

### Common Operations

| Operation | Formula | Code |
|-----------|---------|------|
| Distance | `sqrt((x2-x1)^2 + (y2-y1)^2)` | `Vector2.Distance(a, b)` |
| Normalize | `v / length(v)` | `v.normalized` |
| Dot product | `a.x*b.x + a.y*b.y` | `Vector2.Dot(a, b)` |
| Lerp | `a + (b - a) * t` | `Vector2.Lerp(a, b, t)` |
| Angle | `atan2(dy, dx)` | `Mathf.Atan2(dy, dx)` |

### Collision Detection

| Method | When | Cost |
|--------|------|------|
| AABB | Simple boxes, fast | Very cheap |
| Circle | Round objects | Cheap |
| SAT | Convex polygons | Medium |
| Raycast | Line of sight | Cheap |
| Broad phase | Reduce checks | Varies |

## Common Mistakes

| Mistake | Problem | Solution |
|---------|---------|----------|
| Game logic in Update | Tied to framerate | Use FixedUpdate for physics |
| Not pooling objects | GC spikes, lag | Object pooling for bullets/particles |
| Hardcoded values | Hard to tune | Use ScriptableObjects/config |
| Deep inheritance | Brittle, hard to extend | Use composition/ECS |
| Not using delta time | Speed varies with framerate | Multiply by `deltaTime` |
| Ignoring input buffering | Unresponsive controls | Buffer input for a few frames |

---

> **Full section:** [Game Development](../14-game-development/README.md) | **Next:** [Machine Learning](ml-quick-reference.md)
