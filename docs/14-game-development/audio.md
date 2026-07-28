# Audio

> Sound effects, music, spatial audio, and mixing — making your game sound as good as it looks.

---

## What Is It?

Audio in games includes sound effects (SFX), music, ambient sounds, and voice. Good audio provides feedback, atmosphere, and emotional impact. Bad audio (or no audio) makes a game feel unfinished.

> **Related:** [UI](ui.md) for UI sounds. [Performance](performance.md) for audio optimization.

---

## Why Does It Matter?

| Without Audio | With Audio |
|---------------|------------|
| Silent, lifeless game | Immersive experience |
| No feedback on actions | Instant confirmation |
| No atmosphere | Mood and tension |
| Feels unfinished | Polished and professional |

## Audio Types

| Type | Examples | Priority |
|------|----------|----------|
| **SFX** | Jump, shoot, hit, collect | Essential |
| **Music** | Background soundtrack | High |
| **Ambient** | Wind, birds, machinery | Medium |
| **UI** | Button clicks, menu sounds | Medium |
| **Voice** | Dialog, narration | Low (optional) |

## Audio Components

### Audio Source

Plays a sound. Attached to a position in the game world.

```csharp
// Unity
audioSource.PlayOneShot(jumpSound);
audioSource.PlayOneShot(hitSound, 0.5f); // half volume
```

```gdscript
# Godot
$AudioStreamPlayer2D.stream = jump_sound
$AudioStreamPlayer2D.play()
```

### Audio Listener

Receives audio. Usually attached to the camera. Only one per scene.

### Audio Mixer

Controls volume, effects, and routing for groups of sounds.

```
Master
├── SFX
│   ├── Jump
│   ├── Shoot
│   └── Hit
├── Music
│   ├── Main Theme
│   └── Battle Theme
└── Ambient
    ├── Wind
    └── Birds
```

## Spatial Audio

### 2D Panning

Sound moves left/right based on position relative to listener.

```csharp
// Unity - 2D panning (built-in with Audio Source)
audioSource.spatialBlend = 1f; // full 3D
audioSource.panStereo = -0.5f; // left
```

### 3D Attenuation

Sound gets quieter with distance.

| Mode | Behavior |
|------|----------|
| Linear | Decreases linearly |
| Logarithmic | Decreases quickly near, slowly far (realistic) |
| Custom | User-defined curve |

## Pooled Audio

Reuse audio sources instead of creating/destroying them.

```csharp
// Unity - audio pool
public class AudioPool : MonoBehaviour
{
    [SerializeField] private AudioSource[] sources;
    private int currentIndex;

    public void Play(AudioClip clip, float volume = 1f)
    {
        sources[currentIndex].clip = clip;
        sources[currentIndex].volume = volume;
        sources[currentIndex].Play();
        currentIndex = (currentIndex + 1) % sources.Length;
    }
}
```

## Music

### Looping

```csharp
// Unity - loop music
musicSource.clip = backgroundMusic;
musicSource.loop = true;
musicSource.Play();
```

### Crossfade Between Tracks

```gdscript
# Godot - crossfade
func crossfade_to(new_track):
    var tween = create_tween()
    tween.set_parallel(true)
    tween.tween_property($OldPlayer, "volume_db", -40, 1.0)
    tween.tween_property($NewPlayer, "volume_db", 0, 1.0)
    $NewPlayer.stream = new_track
    $NewPlayer.play()
    tween.chain().tween_callback($OldPlayer.stop)
```

## Best Practices

- **Pool audio sources** — Don't create/destroy for each sound
- **Use audio mixers** — Group sounds for volume control
- **Set up spatial audio** — Position matters for immersion
- **Randomize pitch slightly** — Prevents repetitive sounds
- **Compress audio assets** — Reduce memory usage

## Common Mistakes

| Mistake | Problem | Solution |
|---------|---------|----------|
| Creating audio sources per sound | Performance hit | Pool audio sources |
| No volume control | Players can't adjust | Use audio mixers |
| Same pitch every time | Sounds robotic | Randomize pitch ±10% |
| No spatial audio | Sounds flat | Add spatial blend |
| Large audio files | Memory usage | Compress, use streaming |

## Related Topics

- [UI](ui.md) — UI sound effects
- [Performance](performance.md) — Audio optimization
- [Rendering](rendering.md) — Visual feedback alongside audio

## Further Learning

- [Unity Audio](https://docs.unity3d.com/Manual/Audio.html) — Official docs
- [Godot Audio](https://docs.godotengine.org/en/stable/tutorials/audio/index.html) — Official docs
- [FMOD](https://www.fmod.com/) — Professional audio middleware
- [Wwise](https://www.audiokinetic.com/) — Professional audio middleware

---

## Personal Notes

> Add your own notes, reminders, and experiences here.
