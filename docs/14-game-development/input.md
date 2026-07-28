# Input

> Handling player input — keyboard, mouse, gamepad, touch — with buffering, remapping, and responsive controls.

---

## What Is It?

Input handling is how your game reads player actions — key presses, mouse movement, gamepad sticks, and touch. Good input handling feels responsive and supports multiple control schemes.

> **Related:** [Game Loop](game-loop.md) for when input is processed. [UI](ui.md) for UI input vs gameplay input.

---

## Why Does It Matter?

| Bad Input | Good Input |
|-----------|------------|
| Laggy, unresponsive | Frame-perfect responses |
| Only keyboard support | Gamepad, touch, keyboard |
| Hardcoded keys | Remappable controls |
| No feedback | Visual + audio + haptic feedback |

## Input Models

### Polling (Check Every Frame)

Check input state each frame in the update loop.

```csharp
// Unity
void Update()
{
    if (Input.GetKey(KeyCode.Space))
        Jump();
    
    if (Input.GetMouseButtonDown(0))
        Shoot();
    
    float h = Input.GetAxis("Horizontal");
    Move(h);
}
```

```gdscript
# Godot
func _process(delta):
    if Input.is_action_pressed("jump"):
        jump()
    
    if Input.is_action_just_pressed("shoot"):
        shoot()
    
    var h = Input.get_axis("left", "right")
    move(h)
```

### Event-Driven (React to Events)

React to input events as they happen.

```python
# Pygame
for event in pygame.event.get():
    if event.type == pygame.KEYDOWN:
        if event.key == pygame.K_SPACE:
            jump()
    if event.type == pygame.MOUSEBUTTONDOWN:
        if event.button == 1:
            shoot()
```

### Action Maps (Modern Approach)

Define abstract actions, map to physical keys.

```yaml
# Godot InputMap
jump: [Space, W, Up]
left: [A, Left]
right: [D, Right]
shoot: [Mouse Left, Gamepad A]
```

```csharp
// Unity Input System
// Actions defined in Input Actions asset
// jump: Space, W, Gamepad A Button
// move: WASD, Left Stick
```

## Input Buffering

Buffer input for a few frames so fast inputs aren't dropped.

```python
class InputBuffer:
    def __init__(self, buffer_time=0.1):
        self.buffer = {}
        self.buffer_time = buffer_time

    def press(self, action):
        self.buffer[action] = self.buffer_time

    def is_buffered(self, action):
        return action in self.buffer

    def update(self, dt):
        for action in list(self.buffer.keys()):
            self.buffer[action] -= dt
            if self.buffer[action] <= 0:
                del self.buffer[action]

# Usage
buffer = InputBuffer()

def _process(delta):
    if Input.is_action_just_pressed("jump"):
        buffer.press("jump")
    
    if buffer.is_buffered("jump") and is_on_floor():
        jump()
        buffer.clear("jump")
    
    buffer.update(delta)
```

## Remappable Controls

Let players rebind keys.

```python
# Store key bindings
bindings = {
    "jump": pygame.K_SPACE,
    "left": pygame.K_a,
    "right": pygame.K_d,
    "shoot": pygame.K_z,
}

def rebind(action, new_key):
    bindings[action] = new_key

def is_action_pressed(action):
    key = bindings.get(action)
    return key and pygame.key.get_pressed()[key]
```

## Gamepad Support

### Analog Stick Processing

```python
# Deadzone (ignore small movements)
def process_stick(x, y, deadzone=0.2):
    magnitude = math.sqrt(x*x + y*y)
    if magnitude < deadzone:
        return 0, 0
    # Normalize to 0-1 range
    normalized = (magnitude - deadzone) / (1.0 - deadzone)
    return x/magnitude * normalized, y/magnitude * normalized
```

### Vibration

```csharp
// Unity
Gamepad.current.SetMotorSpeeds(lowSpeed, highSpeed);
// Stop after duration
StartCoroutine(StopVibration(duration));
```

## Touch Input

```gdscript
# Godot - touch
func _input(event):
    if event is InputEventScreenTouch:
        if event.pressed:
            handle_touch_start(event.position)
        else:
            handle_touch_end(event.position)
    
    if event is InputEventScreenDrag:
        handle_touch_drag(event.position)
```

## Best Practices

- **Support multiple input methods** — Keyboard, gamepad, touch
- **Use abstract actions, not raw keys** — "jump" not "Space"
- **Add input buffering** — 100ms buffer prevents dropped inputs
- **Allow remapping** — Accessibility and preference
- **Add visual feedback** — Show what button to press
- **Handle edge cases** — Multiple inputs, focus loss, disconnects

## Common Mistakes

| Mistake | Problem | Solution |
|---------|---------|----------|
| Hardcoded keys | Can't remap | Use action maps |
| No input buffer | Dropped inputs | Add 100ms buffer |
| Checking in FixedUpdate | Missed inputs | Check in Update, apply in FixedUpdate |
| No gamepad support | Alienates players | Add gamepad from the start |
| No deadzone on sticks | Jittery movement | Apply deadzone filtering |

## Related Topics

- [Game Loop](game-loop.md) — When input is processed
- [UI](ui.md) — UI input vs gameplay input
- [2D Math](2d-math.md) — Vector math for movement

## Further Learning

- [Unity Input System](https://docs.unity3d.com/Packages/com.unity.inputsystem@latest) — Official docs
- [Godot Input](https://docs.godotengine.org/en/stable/tutorials/scripting/input.html) — Official docs

---

## Personal Notes

> Add your own notes, reminders, and experiences here.
