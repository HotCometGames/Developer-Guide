# 2D Math

> The essential math for game development — vectors, transformations, collision detection, and interpolation.

---

## What Is It?

2D math is the foundation of all game movement, collision, and rendering. Every time an entity moves, rotates, or collides, vector math is happening behind the scenes.

> **Related:** [Physics](physics.md) for applying math to physics. [Game Loop](game-loop.md) for delta time in movement.

---

## Why Does It Matter?

| Without Math | With Math |
|--------------|-----------|
| Hardcoded positions | Dynamic, relative movement |
| Frame-dependent speed | Frame-rate independent motion |
| Manual collision checks | Mathematical collision detection |
| Jerky animations | Smooth interpolation |

## Vectors

A vector is a direction with magnitude (length). In 2D, it's an `(x, y)` pair.

### Common Operations

| Operation | Formula | Code |
|-----------|---------|------|
| Add | `(a.x+b.x, a.y+b.y)` | `a + b` |
| Subtract | `(a.x-b.x, a.y-b.y)` | `a - b` |
| Scale | `(a.x*s, a.y*s)` | `a * s` |
| Length | `sqrt(x*x + y*y)` | `vector.length()` |
| Normalize | `(x/len, y/len)` | `vector.normalized` |
| Dot product | `a.x*b.x + a.y*b.y` | `Vector2.dot(a, b)` |
| Distance | `length(a - b)` | `Vector2.distance(a, b)` |

### When to Use Each

| Operation | Use Case |
|-----------|----------|
| Add | Combining movements (walk + jump) |
| Subtract | Finding direction between two points |
| Scale | Speed, acceleration, forces |
| Normalize | Getting direction without magnitude |
| Dot product | Angle between vectors, lighting |
| Distance | Range checks, proximity |

### Code Examples

```python
import math

class Vector2:
    def __init__(self, x=0, y=0):
        self.x = x
        self.y = y

    def __add__(self, other):
        return Vector2(self.x + other.x, self.y + other.y)

    def __sub__(self, other):
        return Vector2(self.x - other.x, self.y - other.y)

    def __mul__(self, scalar):
        return Vector2(self.x * scalar, self.y * scalar)

    def length(self):
        return math.sqrt(self.x * self.x + self.y * self.y)

    def normalized(self):
        lng = self.length()
        if lng == 0:
            return Vector2(0, 0)
        return Vector2(self.x / lng, self.y / lng)

    def dot(self, other):
        return self.x * other.x + self.y * other.y

    def distance_to(self, other):
        return (self - other).length()
```

```csharp
// Unity
Vector2 direction = (target.position - transform.position).normalized;
float distance = Vector2.Distance(transform.position, target.position);
float dot = Vector2.Dot(transform.up, direction);
```

```gdscript
# Godot
var direction = (target.position - position).normalized()
var distance = position.distance_to(target.position)
var dot = transform.y.dot(direction)
```

## Transformations

### Translation (Moving)

```python
# Move toward target at speed
direction = (target - position).normalized()
position += direction * speed * delta_time
```

### Rotation

| Concept | Formula | Code |
|---------|---------|------|
| Rotate point | `x' = x*cos - y*sin`, `y' = x*sin + y*cos` | `Vector2(x*c - y*s, x*s + y*c)` |
| Angle to direction | `(cos(angle), sin(angle))` | `Vector2(cos(a), sin(a))` |
| Direction to angle | `atan2(dy, dx)` | `math.atan2(dy, dx)` |

```python
import math

def rotate_point(point, angle):
    c = math.cos(angle)
    s = math.sin(angle)
    return Vector2(
        point.x * c - point.y * s,
        point.x * s + point.y * c
    )

def angle_to_direction(angle):
    return Vector2(math.cos(angle), math.sin(angle))

def direction_to_angle(direction):
    return math.atan2(direction.y, direction.x)
```

### Scale

```python
# Uniform scale
scaled = vector * 2.0

# Non-uniform scale
scaled = Vector2(vector.x * 2.0, vector.y * 1.0)
```

## Collision Detection

### AABB (Axis-Aligned Bounding Box)

Two rectangles that aren't rotated.

```python
class AABB:
    def __init__(self, x, y, width, height):
        self.x = x
        self.y = y
        self.width = width
        self.height = height

    def intersects(self, other):
        return (
            self.x < other.x + other.width and
            self.x + self.width > other.x and
            self.y < other.y + other.height and
            self.y + self.height > other.y
        )
```

### Circle Collision

```python
def circles_collide(pos1, radius1, pos2, radius2):
    distance = pos1.distance_to(pos2)
    return distance < radius1 + radius2
```

### Raycasting

```python
def ray_intersects_circle(origin, direction, center, radius):
    oc = origin - center
    a = direction.dot(direction)
    b = 2 * oc.dot(direction)
    c = oc.dot(oc) - radius * radius
    discriminant = b * b - 4 * a * c

    if discriminant < 0:
        return None

    t = (-b - math.sqrt(discriminant)) / (2 * a)
    if t < 0:
        t = (-b + math.sqrt(discriminant)) / (2 * a)
    if t < 0:
        return None

    return origin + direction * t
```

### Collision Methods Comparison

| Method | When | Cost | Accuracy |
|--------|------|------|----------|
| AABB | Rectangular objects | Very cheap | Low (boxes only) |
| Circle | Round objects | Cheap | Low (circles only) |
| SAT | Convex polygons | Medium | High (exact) |
| Raycast | Line of sight, shooting | Cheap | Exact along ray |
| Broad phase | Reduce collision checks | Varies | Pre-filter |

## Interpolation

### Lerp (Linear Interpolation)

Smoothly move from A to B.

```python
def lerp(a, b, t):
    return a + (b - a) * t

# Usage: move 5% toward target each frame
position.x = lerp(position.x, target.x, 0.05)
position.y = lerp(position.y, target.y, 0.05)
```

### Smoothstep

Ease-in, ease-out curve.

```python
def smoothstep(t):
    return t * t * (3 - 2 * t)
```

### Easing Functions

| Function | Curve | Use |
|----------|-------|-----|
| Linear | Straight line | Constant speed |
| Ease-in | Slow start, fast end | Acceleration |
| Ease-out | Fast start, slow end | Deceleration |
| Ease-in-out | Slow both ends | Smooth transitions |
| Bounce | Overshoot + settle | playful animations |

## Best Practices

- **Normalize direction vectors** — Always before multiplying by speed
- **Use delta time** — Multiply all movement by `delta`
- **Use built-in vector types** — Unity `Vector2`, Godot `Vector2`, not raw tuples
- **Cache math results** — Don't recompute `sin`/`cos` every frame
- **Use magnitude squared for distance checks** — Avoid `sqrt` when possible

## Common Mistakes

| Mistake | Problem | Solution |
|---------|---------|----------|
| Not normalizing direction | Speed varies with distance | `.normalized()` before `* speed` |
| Using position for direction | Wrong direction vector | `target - position`, then normalize |
| Comparing floats exactly | Never equals due to precision | Use epsilon: `abs(a - b) < 0.001` |
| Forgetting delta time | Speed tied to frame rate | Always multiply by `delta` |
| Angle in degrees vs radians | Wrong rotation | Check your engine's convention |

## Related Topics

- [Physics](physics.md) — Applying math to physics simulation
- [Game Loop](game-loop.md) — Delta time in movement
- [Rendering](rendering.md) — Transforms for drawing

## Further Learning

- [Red Blob Games](https://www.redblobgames.com/) — Interactive math tutorials
- [Vector Math](https://www.youtube.com/watch?v=keJN_PqvrmY) — Visual explanations
- [Game Math Book](https://gamemath.com/) — Free online resource

---

## Personal Notes

> Add your own notes, reminders, and experiences here.
