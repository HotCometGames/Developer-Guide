# Rendering

> Drawing your game — sprites, animations, cameras, draw calls, and the visual pipeline.

---

## What Is It?

Rendering is the process of drawing everything to the screen each frame. In 2D games, this means drawing sprites, animations, UI, and effects in the correct order with the right transformations.

> **Related:** [Game Loop](game-loop.md) for when rendering happens. [2D Math](2d-math.md) for transforms used in rendering.

---

## Why Does It Matter?

| Poor Rendering | Good Rendering |
|----------------|----------------|
| Janky, unpolished visuals | Smooth, professional look |
| Low frame rate | Optimized draw calls |
| No visual feedback | Particles, screen shake, juice |
| Hardcoded positions | Flexible camera and parallax |

## Sprites

### What Is a Sprite?

A sprite is a 2D image rendered on screen. Sprites can be static images or part of an animation (sprite sheet).

### Sprite Sheet

Multiple animation frames packed into one image.

```
Sprite Sheet (4 frames of walk animation):
+------+------+------+------+
| F1   | F2   | F3   | F4   |
+------+------+------+------+
```

### Sprite Rendering

```csharp
// Unity - draw sprite at position
spriteRenderer.sprite = walkFrames[currentFrame];
spriteRenderer.flipX = facingLeft;
```

```gdscript
# Godot - draw sprite
$Sprite2D.texture = walk_frames[current_frame]
$Sprite2D.flip_h = facing_left
```

## Animation

### Frame-Based Animation

```csharp
// Unity - simple frame animation
public class Animation : MonoBehaviour
{
    [SerializeField] private Sprite[] frames;
    [SerializeField] private float frameRate = 10f;
    
    private float timer;
    private int currentFrame;

    void Update()
    {
        timer += Time.deltaTime;
        if (timer >= 1f / frameRate)
        {
            timer = 0;
            currentFrame = (currentFrame + 1) % frames.Length;
            GetComponent<SpriteRenderer>().sprite = frames[currentFrame];
        }
    }
}
```

### Godot AnimationPlayer

```
# Built-in AnimationEditor
# Keyframe any property over time
# Supports: position, rotation, scale, frame, modulate, etc.
```

### Tweening

```gdscript
# Godot - tween animation
var tween = create_tween()
tween.tween_property($Sprite2D, "position", target_pos, 0.5)
tween.tween_property($Sprite2D, "scale", Vector2(1.2, 1.2), 0.1)
tween.tween_property($Sprite2D, "scale", Vector2(1, 1), 0.1)
```

```csharp
// Unity - DOTween (popular tween library)
transform.DOMove(targetPos, 0.5f);
transform.DOScale(1.2f, 0.1f).OnComplete(() => 
    transform.DOScale(1f, 0.1f));
```

## Cameras

### Camera Follow

```csharp
// Unity - smooth camera follow
public class CameraFollow : MonoBehaviour
{
    [SerializeField] private Transform target;
    [SerializeField] private float smoothSpeed = 0.125f;
    [SerializeField] private Vector3 offset = new Vector3(0, 0, -10);

    void LateUpdate()
    {
        Vector3 desired = target.position + offset;
        Vector3 smoothed = Vector3.Lerp(
            transform.position, desired, smoothSpeed
        );
        transform.position = smoothed;
    }
}
```

```gdscript
# Godot - camera follow
func _process(delta):
    var target_pos = player.global_position + offset
    global_position = global_position.lerp(target_pos, smoothing * delta)
```

### Camera Bounds

```csharp
// Unity - clamp camera to bounds
void LateUpdate()
{
    Vector3 pos = transform.position;
    pos.x = Mathf.Clamp(pos.x, minX, maxX);
    pos.y = Mathf.Clamp(pos.y, minY, maxY);
    transform.position = pos;
}
```

### Camera Effects

| Effect | How | When |
|--------|-----|------|
| Screen shake | Random offset for few frames | Impact, explosion |
| Zoom | Orthographic size change | Events, transitions |
| Parallax | Layers move at different speeds | Background depth |
| Camera lerp | Smooth follow with lerp | Standard follow |

### Screen Shake

```csharp
// Unity - screen shake
public IEnumerator Shake(float duration, float magnitude)
{
    Vector3 originalPos = transform.localPosition;
    float elapsed = 0f;

    while (elapsed < duration)
    {
        float x = Random.Range(-1f, 1f) * magnitude;
        float y = Random.Range(-1f, 1f) * magnitude;
        transform.localPosition = originalPos + new Vector3(x, y, 0);
        elapsed += Time.deltaTime;
        yield return null;
    }
    transform.localPosition = originalPos;
}
```

## Draw Calls and Batching

### What Is a Draw Call?

Each time the GPU draws something, it's a draw call. Too many draw calls = slow frame rate.

| Count | Frame Rate Impact |
|-------|-------------------|
| Under 100 | Fine |
| 100-500 | Monitor performance |
| 500+ | Optimize needed |

### Optimization Techniques

| Technique | How | Impact |
|-----------|-----|--------|
| Sprite atlases | Pack sprites into one texture | Reduces draw calls |
| Static batching | Merge non-moving objects | Major improvement |
| Sorting layers | Draw order management | Correct visual order |
| Object pooling | Reuse objects, don't recreate | Reduces GC spikes |
| Culling | Don't draw off-screen objects | Major improvement |

## Sorting and Layers

### Draw Order

Objects are drawn back-to-front. Later in the list = drawn on top.

| Layer | Purpose |
|-------|---------|
| Background | Far background elements |
| Parallax BG | Moving background layers |
| Tiles | Ground, walls |
| Items | Pickups, decorations |
| Entities | Players, enemies |
| Foreground | Near elements |
| UI | HUD, menus |

### Unity Sorting Layers

```
Sorting Layers (back to front):
1. Background
2. Default
3. Player
4. UI

Order in Layer: 0, 1, 2, 3...
```

## Best Practices

- **Use sprite atlases** — Pack sprites to reduce draw calls
- **Pool frequently created objects** — Bullets, particles, enemies
- **Cull off-screen objects** — Don't render what you can't see
- **Use sorting layers** — Manage draw order cleanly
- **Separate logic from rendering** — Update position, then render

## Common Mistakes

| Mistake | Problem | Solution |
|---------|---------|----------|
| Too many draw calls | Low frame rate | Use sprite atlases, batching |
| Wrong draw order | Visual glitches | Set up sorting layers |
| Not pooling objects | GC spikes, lag | Object pooling for bullets/particles |
| Camera too tight | Player can't see threats | Add lookahead, padding |
| No screen shake | Impacts feel weak | Add shake on hits |

## Related Topics

- [2D Math](2d-math.md) — Transforms for rendering
- [Game Loop](game-loop.md) — When rendering happens
- [Performance](performance.md) — Optimizing rendering

## Further Learning

- [Unity Rendering](https://docs.unity3d.com/Manual/RenderPipeline.html) — Official docs
- [Godot 2D Rendering](https://docs.godotengine.org/en/stable/tutorials/2d/2d_rendering.html) — Official docs

---

## Personal Notes

> Add your own notes, reminders, and experiences here.
