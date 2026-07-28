# Game Loop

> The core architecture of every game — how the loop works, fixed vs variable timestep, and frame rate independence.

---

## What Is It?

The game loop is the heartbeat of your game. It's a `while` loop that runs from startup to shutdown, processing input, updating game state, and rendering frames. Every single thing that happens in your game happens inside this loop.

> **Related:** [What Is Game Dev?](what-is-gamedev.md) for the mental model. [Physics](physics.md) for why FixedUpdate matters.

---

## Why Does It Matter?

| Without a Proper Loop | With a Proper Loop |
|----------------------|-------------------|
| Game runs at different speeds on different hardware | Consistent behavior everywhere |
| Physics breaks at low frame rates | Physics runs at fixed rate |
| Input feels laggy | Responsive controls |
| Gameplay tied to rendering | Clean separation of concerns |

## The Basic Loop

```
initialize()
while game_is_running:
    process_input()
    update_game_state(delta_time)
    render()
cleanup()
```

### Delta Time

Delta time (`dt`) is the time elapsed since the last frame. It's what makes your game frame-rate independent.

| Frame Rate | Delta Time | Movement per Frame | Movement per Second |
|------------|-----------|-------------------|---------------------|
| 30 FPS | 0.033s | 0.033 * 200 = 6.6 | 200 units |
| 60 FPS | 0.017s | 0.017 * 200 = 3.3 | 200 units |
| 144 FPS | 0.007s | 0.007 * 200 = 1.4 | 200 units |

Without delta time, a character moving 5 pixels per frame moves 3x faster at 144 FPS than at 30 FPS.

## Timestep Strategies

### Fixed Timestep

The update runs at a fixed interval (e.g., 60 times per second), regardless of frame rate.

```python
fixed_dt = 1/60
accumulator = 0

while running:
    frame_dt = get_frame_time()
    accumulator += frame_dt
    
    while accumulator >= fixed_dt:
        process_input()
        update(fixed_dt)
        accumulator -= fixed_dt
    
    render(accumulator / fixed_dt)  # for interpolation
```

| Pros | Cons |
|------|------|
| Deterministic (same result every run) | May skip updates on slow machines |
| Physics works correctly | Extra updates cause lag spikes |
| Easy to reason about | Doesn't handle variable frame times |

### Variable Timestep

The update runs once per frame, using the actual delta time.

```python
while running:
    dt = get_frame_time()
    process_input()
    update(dt)
    render()
```

| Pros | Cons |
|------|------|
| Simple to implement | Non-deterministic physics |
| Uses all available CPU | Physics can break at low FPS |
| Smooth on all hardware | Movement feels inconsistent |

### Semi-Fixed Timestep (Recommended)

Physics runs at fixed rate, everything else runs at frame rate.

```python
physics_dt = 1/60
accumulator = 0

while running:
    frame_dt = get_frame_time()
    accumulator += frame_dt
    
    process_input()
    
    while accumulator >= physics_dt:
        update_physics(physics_dt)
        accumulator -= physics_dt
    
    update_gameplay(frame_dt)  # rendering, UI, animations
    render()
```

| Pros | Cons |
|------|------|
| Physics is stable | More complex to implement |
| Rendering is smooth | Need to separate physics from gameplay |
| Best of both worlds | Interpolation needed for smooth visuals |

## Engine Implementations

### Unity

| Method | Rate | Use For |
|--------|------|---------|
| `Update()` | Every frame | Input, animations, UI |
| `FixedUpdate()` | 60 Hz (default) | Physics, Rigidbody movement |
| `LateUpdate()` | After all Updates | Camera follow, final adjustments |
| `FixedUpdate` + `Update` | Combined | Semi-fixed timestep |

```csharp
// Frame-rate independent movement
void Update()
{
    transform.position += direction * speed * Time.deltaTime;
}

// Physics at fixed rate
void FixedUpdate()
{
    rb.AddForce(force * Time.fixedDeltaTime);
}
```

### Godot

| Method | Rate | Use For |
|--------|------|---------|
| `_process(delta)` | Every frame | Input, animations, UI |
| `_physics_process(delta)` | 60 Hz | Physics, movement |
| `_input(event)` | Per input event | Raw input handling |

```gdscript
func _process(delta):
    # Frame-rate independent animation
    sprite.rotation += rotation_speed * delta

func _physics_process(delta):
    # Physics at fixed rate
    velocity.y += gravity * delta
    move_and_slide()
```

### Pygame (Manual)

```python
import pygame
import sys

clock = pygame.time.Clock()
FIXED_DT = 1/60
accumulator = 0

while running:
    frame_dt = clock.tick(60) / 1000  # cap at 60 FPS
    accumulator += frame_dt
    
    for event in pygame.event.get():
        handle_input(event)
    
    while accumulator >= FIXED_DT:
        update_physics(FIXED_DT)
        accumulator -= FIXED_DT
    
    update_game(frame_dt)
    render()
    pygame.display.flip()
```

## Frame Rate

| Frame Rate | Delta Time | Feel |
|------------|-----------|------|
| 30 FPS | 33ms | Playable, slightly sluggish |
| 60 FPS | 17ms | Standard, smooth |
| 120 FPS | 8ms | Very smooth, competitive |
| 144 FPS | 7ms | Monitor limit, esports |

### Capping Frame Rate

```python
# Pygame
clock.tick(60)  # cap at 60 FPS

# Unity
Application.targetFrameRate = 60;

# Godot
Engine.max_fps = 60
```

## Best Practices

- **Always use delta time** — Multiply movement by `delta` or `Time.deltaTime`
- **Separate physics from rendering** — Physics at fixed rate, rendering at frame rate
- **Don't do heavy work in the loop** — Move expensive operations to initialization
- **Profile your loop** — Know where time is spent
- **Cap your frame rate** — Prevent wasting CPU/GPU

## Common Mistakes

| Mistake | Problem | Solution |
|---------|---------|----------|
| Not using delta time | Speed varies with FPS | `position += velocity * delta` |
| Physics in Update | Unstable at variable FPS | Use FixedUpdate for physics |
| Heavy work in Update | Frame drops | Move to initialization or async |
| Not capping frame rate | 100% GPU usage, hot laptop | Cap at monitor refresh rate |
| Assuming 60 FPS | Breaks on slower machines | Always use delta time |

## Related Topics

- [Physics](physics.md) — Why FixedUpdate matters for physics
- [2D Math](2d-math.md) — Vector math for movement
- [Performance](performance.md) — Optimizing the game loop

## Further Learning

- [Fix Your Timestep](https://gafferongames.com/post/fix_your_timestep/) — Gaffer on Games (essential reading)
- [Game Loop Patterns](https://gameprogrammingpatterns.com/game-loop.html) — Game Programming Patterns

---

## Personal Notes

> Add your own notes, reminders, and experiences here.
