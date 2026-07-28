# Performance

> Profiling, optimization, object pooling, LOD, and keeping your game running smooth.

---

## What Is It?

Game performance is measured in frames per second (FPS). Drops below 30 FPS feel sluggish. The goal is a consistent 60 FPS (or higher). Performance work means finding bottlenecks and fixing them.

> **Related:** [Game Loop](game-loop.md) for frame rate basics. [Rendering](rendering.md) for draw call optimization.

---

## Why Does It Matter?

| Poor Performance | Good Performance |
|------------------|-----------------|
| Frame drops, stuttering | Smooth, consistent frame rate |
| Players quit | Players stay engaged |
| Crashes on low-end hardware | Runs on wide range of devices |
| Unprofessional feel | Polished experience |

## Profiling

### What to Measure

| Metric | Target | Tool |
|--------|--------|------|
| Frame time | Under 16.7ms (60 FPS) | Profiler |
| Draw calls | Under 100-200 | Frame debugger |
| Memory | Under budget | Memory profiler |
| GC allocations | Minimal per frame | Profiler |

### Unity Profiler

```
Window > Analysis > Profiler
- CPU Usage: See what takes time per frame
- GPU: Rendering bottleneck
- Memory: Allocations, leaks
- Audio: Audio system cost
```

### Godot Monitor

```
Debugger > Monitors
- FPS: Current frame rate
- Process: CPU time per frame
- Physics: Physics time per frame
- Objects: Active object count
- Video memory: GPU memory usage
```

## Common Bottlenecks

| Bottleneck | Symptom | Fix |
|------------|---------|-----|
| **CPU: Logic** | High script time | Simplify AI, reduce calculations |
| **CPU: Physics** | High FixedUpdate time | Reduce collision checks, simplify shapes |
| **CPU: GC** | Frame spikes every few seconds | Pool objects, reduce allocations |
| **GPU: Draw calls** | High render time | Sprite atlases, batching |
| **GPU: Overdraw** | Transparent pixels drawn many times | Reduce transparent objects |
| **Memory** | Crashes, slow loading | Compress textures, pool objects |

## Object Pooling

Reuse objects instead of creating and destroying them.

```python
class ObjectPool:
    def __init__(self, scene, initial_size=20):
        self.scene = scene
        self.available = []
        self.active = []
        
        for _ in range(initial_size):
            obj = scene.instantiate()
            obj.visible = false
            obj.process_mode = Node.PROCESS_MODE_DISABLED
            self.available.append(obj)

    def get(self):
        if self.available:
            obj = self.available.pop()
        else:
            obj = self.scene.instantiate()
        
        obj.visible = true
        obj.process_mode = Node.PROCESS_MODE_INHERIT
        self.active.append(obj)
        return obj

    def release(self, obj):
        obj.visible = false
        obj.process_mode = Node.PROCESS_MODE_DISABLED
        obj.global_position = Vector2(-1000, -1000)
        self.active.remove(obj)
        self.available.append(obj)
```

### What to Pool

| Object | Frequency | Impact |
|--------|-----------|--------|
| Bullets/projectiles | Very high | Critical |
| Particles | High | High |
| Enemies | Medium | Medium |
| Damage numbers | High | Medium |
| Audio sources | High | Medium |

## Level of Detail (LOD)

Reduce detail for distant objects.

| Level | Detail | Distance |
|-------|--------|----------|
| LOD 0 | Full detail | Close |
| LOD 1 | Reduced | Medium |
| LOD 2 | Minimal | Far |
| Cull | Hidden | Very far |

## Texture Optimization

| Technique | Impact |
|-----------|--------|
| Compress textures | Reduces memory, faster loading |
| Use power-of-2 sizes | Better GPU compatibility |
| Sprite atlases | Fewer draw calls |
| Mipmaps | Better rendering at distance |
| Resize to target | Don't use 4K for 64px sprites |

## Culling

Don't render what you can't see.

| Type | How |
|------|-----|
| Frustum culling | Don't render outside camera view |
| Occlusion culling | Don't render behind walls |
| Distance culling | Don't render far objects |
| Layer culling | Skip certain layers at distance |

## Best Practices

- **Profile before optimizing** — Find the actual bottleneck
- **Pool frequently created objects** — Bullets, particles, enemies
- **Compress textures** — Always
- **Use sprite atlases** — Reduce draw calls
- **Minimize per-frame allocations** — No `new` in Update loops
- **Test on target hardware** — Your dev PC is faster than players' devices

## Common Mistakes

| Mistake | Problem | Solution |
|---------|---------|----------|
| Optimizing without profiling | Wasted effort | Profile first |
| Creating objects in Update | GC spikes | Object pooling |
| Not compressing textures | Memory bloat | Always compress |
| Too many draw calls | Low frame rate | Sprite atlases |
| Not testing on low-end | Players can't run it | Test on target hardware |

## Related Topics

- [Game Loop](game-loop.md) — Frame rate and delta time
- [Rendering](rendering.md) — Draw calls and batching
- [Physics](physics.md) — Optimizing collision checks

## Further Learning

- [Unity Profiler](https://docs.unity3d.com/Manual/Profiler.html) — Official docs
- [Godot Performance](https://docs.godotengine.org/en/stable/tutorials/performance/index.html) — Official docs
- [Optimizing Games](https://gameprogrammingpatterns.com/data-locality.html) — Data-oriented design

---

## Personal Notes

> Add your own notes, reminders, and experiences here.
