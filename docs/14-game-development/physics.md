# Physics

> How physics engines work — rigidbodies, colliders, collision response, and common game physics patterns.

---

## What Is It?

Game physics simulates real-world forces: gravity, friction, collisions, and joints. A physics engine handles collision detection (did they hit?) and collision response (what happens next?) so you don't have to write it from scratch.

> **Related:** [2D Math](2d-math.md) for the underlying math. [Game Loop](game-loop.md) for why physics runs at a fixed rate.

---

## Why Does It Matter?

| Without Physics Engine | With Physics Engine |
|------------------------|---------------------|
| Write your own collision math | Built-in collision detection |
| Manual gravity and friction | Realistic forces for free |
| Hardcoded responses | Physically plausible behavior |
| Hours of math debugging | Works out of the box |

## Core Concepts

### Rigidbody

A component that enables physics simulation. Without it, objects are static.

| Property | What It Does |
|----------|-------------|
| Mass | How heavy the object is |
| Velocity | Current speed and direction |
| Drag | Air resistance (slows down) |
| Angular Drag | Rotational air resistance |
| Gravity Scale | Multiplier for gravity |
| Body Type | Dynamic (moves), Kinematic (scripted), Static (never moves) |

### Collider

A shape that defines the physical boundary of an object.

| Shape | Use Case | Cost |
|-------|----------|------|
| Box | Rectangular objects | Very cheap |
| Circle | Round objects | Cheap |
| Polygon | Complex 2D shapes | Medium |
| Mesh | Complex 3D shapes | Expensive |

### Trigger vs Collider

| Type | Physics Response | Detection |
|------|-----------------|-----------|
| Collider | Objects bounce off each other | `OnCollisionEnter` |
| Trigger | Objects pass through, but detect overlap | `OnTriggerEnter` |

## Unity Physics

### Setup

```csharp
// Add components to a GameObject
// 1. Rigidbody2D (enables physics)
// 2. Collider2D (defines shape)

public class PlayerMovement : MonoBehaviour
{
    [SerializeField] private float speed = 5f;
    [SerializeField] private float jumpForce = 10f;
    
    private Rigidbody2D rb;

    void Start()
    {
        rb = GetComponent<Rigidbody2D>();
    }

    void FixedUpdate()
    {
        float horizontal = Input.GetAxis("Horizontal");
        rb.linearVelocity = new Vector2(horizontal * speed, rb.linearVelocity.y);
    }

    void Update()
    {
        if (Input.GetButtonDown("Jump") && IsGrounded())
        {
            rb.AddForce(Vector2.up * jumpForce, ForceMode2D.Impulse);
        }
    }

    bool IsGrounded()
    {
        RaycastHit2D hit = Physics2D.Raycast(
            transform.position, Vector2.down, 1.1f
        );
        return hit.collider != null;
    }
}
```

### Collision Events

```csharp
void OnCollisionEnter2D(Collision2D collision)
{
    // Called when this object hits another collider
    if (collision.gameObject.CompareTag("Enemy"))
    {
        TakeDamage(10);
    }
}

void OnTriggerEnter2D(Collider2D other)
{
    // Called when this object enters a trigger
    if (other.CompareTag("Coin"))
    {
        CollectCoin(other.gameObject);
    }
}
```

## Godot Physics

### Setup

```gdscript
extends CharacterBody2D

@export var speed: float = 200.0
@export var jump_force: float = -300.0

var gravity = ProjectSettings.get_setting("physics/2d/default_gravity")

func _physics_process(delta):
    # Apply gravity
    if not is_on_floor():
        velocity.y += gravity * delta

    # Jump
    if Input.is_action_just_pressed("jump") and is_on_floor():
        velocity.y = jump_force

    # Horizontal movement
    var direction = Input.get_axis("left", "right")
    velocity.x = direction * speed

    move_and_slide()
```

### Collision Detection

```gdscript
func _on_area_entered(area):
    if area.is_in_group("coins"):
        area.queue_free()
        coins += 1

func _on_body_entered(body):
    if body.is_in_group("enemies"):
        take_damage(10)
```

## Common Physics Patterns

### Platformer Movement

```csharp
// Unity - smooth platformer
void FixedUpdate()
{
    // Horizontal movement
    float targetSpeed = Input.GetAxisRaw("Horizontal") * maxSpeed;
    float speedDif = targetSpeed - rb.linearVelocity.x;
    float accelRate = Mathf.Abs(targetSpeed) > 0.01f ? acceleration : deceleration;
    float movement = speedDif * accelRate;
    rb.AddForce(movement * Vector2.right);
}
```

### Top-Down Movement

```gdscript
# Godot - top-down with friction
func _physics_process(delta):
    var input = Input.get_vector("left", "right", "up", "down")
    velocity = velocity.move_toward(input * max_speed, acceleration * delta)
    
    if input == Vector2.ZERO:
        velocity = velocity.move_toward(Vector2.ZERO, friction * delta)
    
    move_and_slide()
```

### Projectile

```csharp
// Unity - simple projectile
public class Projectile : MonoBehaviour
{
    [SerializeField] private float speed = 20f;
    [SerializeField] private float lifetime = 3f;

    void Start()
    {
        GetComponent<Rigidbody2D>().linearVelocity = transform.up * speed;
        Destroy(gameObject, lifetime);
    }
}
```

### Object Pooling for Projectiles

```python
class ObjectPool:
    def __init__(self, create_func, initial_size=20):
        self.create_func = create_func
        self.available = [create_func() for _ in range(initial_size)]
        self.active = []

    def get(self):
        if self.available:
            obj = self.available.pop()
        else:
            obj = self.create_func()
        self.active.append(obj)
        return obj

    def release(self, obj):
        if obj in self.active:
            self.active.remove(obj)
            obj.reset()
            self.available.append(obj)
```

## Physics Materials

| Property | What It Does | Range |
|----------|-------------|-------|
| Friction | Resistance to sliding | 0 (ice) to 1 (rubber) |
| Bounciness | How much it bounces | 0 (no bounce) to 1 (full bounce) |
| Friction Combine | How friction combines | Average, Minimum, Maximum, Multiply |
| Bounce Combine | How bounciness combines | Average, Minimum, Maximum, Multiply |

## Joints

| Joint | What It Does | Use Case |
|-------|-------------|----------|
| Hinge | Rotates around a point | Doors, wheels, pendulums |
| Spring | Connects with spring force | Bouncy objects, ropes |
| Distance | Maintains fixed distance | Chains, ragdolls |
| Motor | Applies rotation force | Wheels, gears |

## Best Practices

- **Use FixedUpdate for physics** — Physics must run at fixed rate
- **Use AddForce for movement** — Not direct position manipulation
- **Layer your collisions** — Don't check every object against every other
- **Use triggers for zones** — Coins, doors, damage areas
- **Pool frequently created objects** — Bullets, particles, enemies

## Common Mistakes

| Mistake | Problem | Solution |
|---------|---------|----------|
| Physics in Update | Unstable simulation | Use FixedUpdate |
| Setting velocity directly | Bypasses physics | Use AddForce |
| Too many colliders | Performance hit | Simplify shapes, use layers |
| Not using triggers | Can't detect overlaps | Use triggers for detection |
| Fighting the physics engine | Jittery movement | Work with forces, not against |

## Related Topics

- [2D Math](2d-math.md) — Vector math used by physics
- [Game Loop](game-loop.md) — Fixed timestep for physics
- [Performance](performance.md) — Optimizing physics checks

## Further Learning

- [Unity Physics2D](https://docs.unity3d.com/Manual/Physics2DReference.html) — Official docs
- [Godot Physics](https://docs.godotengine.org/en/stable/tutorials/physics/physics_introduction.html) — Official docs
- [Fix Your Timestep](https://gafferongames.com/post/fix_your_timestep/) — Essential reading

---

## Personal Notes

> Add your own notes, reminders, and experiences here.
