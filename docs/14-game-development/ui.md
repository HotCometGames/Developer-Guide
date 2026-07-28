# UI

> Game user interfaces — HUD, menus, health bars, inventory, and canvas systems.

---

## What Is It?

Game UI is everything the player sees and interacts with that isn't the game world itself: health bars, score displays, menus, dialog boxes, inventories, and pause screens.

> **Related:** [Input](input.md) for UI input handling. [Rendering](rendering.md) for draw order.

---

## Why Does It Matter?

| Bad UI | Good UI |
|--------|---------|
| Confusing, cluttered | Clean, intuitive |
| Hard to read | Clear information hierarchy |
| No feedback | Instant feedback on actions |
| Breaks immersion | Fits the game's style |

## UI Types

| Type | Purpose | Examples |
|------|---------|----------|
| **HUD** | Persistent in-game info | Health, ammo, score, minimap |
| **Menu** | Navigation and settings | Main menu, options, pause |
| **Dialog** | Narrative delivery | NPC conversations, cutscenes |
| **Inventory** | Item management | Equipment, crafting, collectibles |
| **Popup** | Temporary notifications | Achievement, level up, damage numbers |

## Canvas Systems

### Unity Canvas

| Render Mode | Use Case |
|-------------|----------|
| Screen Space - Overlay | HUD, always on top |
| Screen Space - Camera | UI affected by camera |
| World Space | UI in the game world (3D health bars) |

### Godot Control Nodes

```
Control (root)
├── VBoxContainer
│   ├── HBoxContainer
│   │   ├── HealthBar (TextureProgressBar)
│   │   └── HealthLabel (Label)
│   └── ScoreLabel (Label)
└── PauseMenu (hidden)
    ├── VBoxContainer
    │   ├── ResumeButton (Button)
    │   └── QuitButton (Button)
```

## Common UI Components

### Health Bar

```gdscript
# Godot - health bar
@export var max_health: int = 100
var current_health: int = 100

func update_health(value: int):
    current_health = clamp(value, 0, max_health)
    $HealthBar.value = current_health
    $HealthBar.max_value = max_health
    
    # Color based on health percent
    var percent = current_health / max_health
    if percent > 0.5:
        $HealthBar.modulate = Color.GREEN
    elif percent > 0.25:
        $HealthBar.modulate = Color.YELLOW
    else:
        $HealthBar.modulate = Color.RED
```

### Score Display

```csharp
// Unity - score with leading zeros
public class ScoreDisplay : MonoBehaviour
{
    [SerializeField] private TextMeshProUGUI scoreText;
    private int score;

    public void AddScore(int amount)
    {
        score += amount;
        scoreText.text = score.ToString("D6"); // 000001
    }
}
```

### Floating Damage Numbers

```gdscript
# Godot - floating damage number
func show_damage(amount: int):
    var label = damage_number_scene.instantiate()
    label.text = str(amount)
    label.global_position = global_position
    get_tree().current_scene.add_child(label)
    
    var tween = create_tween()
    tween.tween_property(label, "position:y", label.position.y - 50, 0.5)
    tween.parallel().tween_property(label, "modulate:a", 0, 0.5)
    tween.tween_callback(label.queue_free)
```

## UI Navigation

### Keyboard/Controller

```gdscript
# Godot - UI navigation
func _input(event):
    if event.is_action_pressed("ui_down"):
        focus_next()
    if event.is_action_pressed("ui_up"):
        focus_previous()
    if event.is_action_pressed("ui_accept"):
        activate_focused()
```

### Focus Management

| Principle | How |
|-----------|-----|
| Visual focus indicator | Highlight selected button |
| Logical tab order | Navigate in expected order |
| Escape to go back | Consistent back behavior |
| Controller support | D-pad navigates menus |

## Responsive Design

```gdscript
# Godot - responsive layout
func _ready():
    var screen_size = get_viewport_rect().size
    if screen_size.x < 1024:
        # Mobile layout
        apply_mobile_layout()
    else:
        # Desktop layout
        apply_desktop_layout()
```

## Best Practices

- **Clear visual hierarchy** — Most important info is most visible
- **Consistent styling** — Same fonts, colors, spacing throughout
- **Controller support** — Test with gamepad from the start
- **Accessible colors** — Don't rely on color alone for information
- **Animate transitions** — Don't just pop UI in/out

## Common Mistakes

| Mistake | Problem | Solution |
|---------|---------|----------|
| Cluttered HUD | Can't see the game | Minimal, essential info only |
| No controller support | Alienates players | Test with gamepad |
| Hardcoded resolution | Breaks on different screens | Use anchors/containers |
| No visual feedback | Actions feel unresponsive | Animate, add sounds |
| Tiny text | Unreadable on TV/phones | Scale with screen size |

## Related Topics

- [Input](input.md) — UI input handling
- [Rendering](rendering.md) — Draw order for UI
- [Audio](audio.md) — UI sound effects

## Further Learning

- [Unity UI](https://docs.unity3d.com/Packages/com.unity.ugui@latest) — Official docs
- [Godot UI](https://docs.godotengine.org/en/stable/tutorials/ui/index.html) — Official docs

---

## Personal Notes

> Add your own notes, reminders, and experiences here.
