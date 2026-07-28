# Game Development Troubleshooting

> Common issues and fixes across Unity, Godot, and general game development.

---

## Unity Issues

| Problem | Cause | Solution |
|---------|-------|----------|
| `NullReferenceException` in Start | Component not attached | Check Inspector, use `[SerializeField]` |
| Object not moving | Missing Rigidbody | Add Rigidbody2D component |
| Collision not detected | Missing collider or wrong layer | Add collider, check layer matrix |
| `Update()` not called | Object disabled or script not attached | Check active state and Inspector |
| Build fails | Missing scene in build settings | Add scene to File > Build Settings |
| Slow frame rate | Too many draw calls | Use sprite atlases, batch |
| Object jittering | Physics in Update | Move to FixedUpdate |
| `DontDestroyOnLoad` not working | Called on child, not root | Call on root object |

## Godot Issues

| Problem | Cause | Solution |
|---------|-------|----------|
| Node not found | Wrong path | Use `$NodeName` or `get_node()` |
| Signal not connected | Not connected in editor | Connect in editor or code |
| `_ready()` not called | Node not in tree | Ensure node is added to scene |
| `move_and_slide()` not working | Wrong node type | Use CharacterBody2D |
| Exported var not showing | Syntax error in script | Check for typos, restart editor |
| Scene won't run | Missing script or node | Check Output for errors |
| Build fails | Missing export template | Download templates in Editor |
| Input not working | Action not defined | Add action in Project Settings > Input Map |

## General Game Dev Issues

### Frame Rate Drops

```
Diagnosis:
1. Profile to find bottleneck (CPU vs GPU)
2. Check draw calls (too many?)
3. Check GC allocations (creating objects per frame?)
4. Check physics (too many colliders?)
5. Check texture sizes (too large?)
```

### Physics Jitter

| Symptom | Cause | Fix |
|---------|-------|-----|
| Objects vibrate | Physics in Update | Use FixedUpdate |
| Objects pass through | Speed too high | Increase collision iterations |
| Inconsistent behavior | Variable timestep | Use fixed timestep |

### Memory Leaks

| Symptom | Cause | Fix |
|---------|-------|-----|
| Growing memory usage | Objects not freed | Pool or destroy properly |
| Crash after long play | Event listeners not removed | Disconnect on destroy |
| Slow loading | Assets not unloaded | Unload unused assets |

### Input Issues

| Symptom | Cause | Fix |
|---------|-------|-----|
| Input missed | Checking in wrong update method | Check in Update, apply in FixedUpdate |
| Input lag | Too much processing per frame | Reduce per-frame work |
| Gamepad not detected | No gamepad support | Add gamepad input handling |

## Debugging Techniques

### Print Debugging

```csharp
// Unity
Debug.Log($"Position: {transform.position}");
Debug.LogWarning($"Low health: {health}");
Debug.LogError($"Something went wrong!");
```

```gdscript
# Godot
print("Position: ", global_position)
printerr("Something went wrong!")
push_warning("Low health: ", health)
```

### Visual Debugging

| Tool | What It Shows |
|------|--------------|
| Unity Scene View | Gizmos, colliders, paths |
| Godot Debug > Visible Collision Shapes | Collider outlines |
| Unity Frame Debugger | Each draw call |
| Unity Profiler | CPU, GPU, memory per frame |

### Breakpoints

```csharp
// Unity - Visual Studio
// Set breakpoint by clicking line number
// Attach to Unity process
// When hit, inspect variables
```

```gdscript
# Godot
# Set breakpoint by clicking line number
# Debug > Breakpoints
# Press F5 to debug
```

## Best Practices

- **Profile first** — Don't guess, measure
- **Test on target hardware** — Your dev PC is faster
- **Use version control** — Git for easy rollback
- **Keep a bug list** — Track and prioritize issues
- **Test edge cases** — Empty input, max values, rapid clicks

## Related Topics

- [Performance](performance.md) — Optimization techniques
- [Game Loop](game-loop.md) — Frame rate and timing
- [Physics](physics.md) — Physics debugging

---

## Personal Notes

> Add your own notes, reminders, and experiences here.
