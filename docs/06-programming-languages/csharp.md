# C#

> A statically-typed, object-oriented language from Microsoft — the primary language for Unity, .NET, and Windows development.

> **Related:** [Choosing a Language](choosing-a-language.md) | [C++](cpp.md)

---

## What Is It?

C# is a modern, statically-typed language that runs on .NET. It's the primary scripting language for Unity game development, the backbone of Windows desktop applications, and a strong contender for web backends and cloud services.

## When to Use C#

| Use Case | Good Fit? |
|----------|-----------|
| Game development (Unity) | Industry standard |
| Windows desktop apps | Excellent |
| Web backend (ASP.NET) | Excellent |
| Cloud services (Azure) | Excellent |
| Mobile apps (Xamarin/MAUI) | Good |
| Cross-platform apps | Good (.NET runs everywhere) |
| Systems programming | Not ideal |

## Key Features

### Strong Static Typing

```csharp
int count = 5;
string name = "Player";
// count = "hello";  // compile error — type safe
```

### LINQ (Language Integrated Query)

Query collections with SQL-like syntax:

```csharp
var numbers = new[] { 1, 2, 3, 4, 5 };
var doubled = numbers.Select(n => n * 2);
var evens = numbers.Where(n => n % 2 == 0);

// Query syntax (alternative)
var result = from n in numbers
             where n > 3
             select n;
```

### Async/Await

```csharp
public async Task<User> GetUserAsync(int id)
{
    using var client = new HttpClient();
    var response = await client.GetStringAsync($"/api/users/{id}");
    return JsonSerializer.Deserialize<User>(response);
}
```

### Properties & Auto-Properties

```csharp
public class Player
{
    public string Name { get; set; }           // auto-property
    public int Health { get; private set; }    // getter public, setter private
    public int MaxHealth { get; } = 100;       // read-only with default

    public string DisplayName => $"{Name} ({Health}/{MaxHealth})";  // expression-bodied
}
```

### Null Safety

```csharp
#nullable enable
string? maybeNull = null;    // nullable reference type
string notNull = "hello";    // non-nullable

if (maybeNull != null)
{
    Console.WriteLine(maybeNull.Length);  // safe access
}
```

## .NET Ecosystem

| Category | Tools |
|----------|-------|
| IDE | Visual Studio, Rider, VS Code |
| Web framework | ASP.NET Core, Blazor |
| Game engine | Unity |
| ORM | Entity Framework Core |
| Testing | xUnit, NUnit, Moq |
| Package manager | NuGet |
| Build system | MSBuild, dotnet CLI |
| Runtime | .NET (cross-platform) |

## Unity-Specific C#

Unity extends C# with its own types and lifecycle:

```csharp
using UnityEngine;

public class PlayerController : MonoBehaviour
{
    public float speed = 5f;

    void Update()
    {
        float move = Input.GetAxis("Horizontal") * Time.deltaTime * speed;
        transform.Translate(move, 0, 0);
    }

    void OnCollisionEnter(Collision collision)
    {
        if (collision.gameObject.CompareTag("Enemy"))
        {
            TakeDamage(10);
        }
    }
}
```

## Common Pitfalls

| Pitfall | Why | Fix |
|---------|-----|-----|
| NullReferenceException | Accessing a null object | Enable nullable reference types. Check for null before access |
| Boxing/unboxing | Value type to object conversion costs performance | Use generics instead of `ArrayList`/`Hashtable` |
| `async void` | Exceptions can't be caught, crashes the process | Use `async Task` except for event handlers |
| Mutable structs | Unexpected behavior when passing by value | Prefer classes or immutable structs (`readonly record struct`) |
| Thread safety | Shared mutable state causes race conditions | Use `lock`, `ConcurrentDictionary`, or immutable data |

## Best Practices

- **Use nullable reference types** — `#nullable enable` catches null bugs at compile time
- **Prefer `record` types** for data containers — value equality, immutability, concise syntax
- **Use `Primary Constructor`** (C# 12) — concise class declarations
- **Write async code** — I/O-bound operations should be `async Task`
- **Use LINQ for collections** — more readable than loops for filtering/transforming
- **Follow Unity lifecycle** — `Awake`, `Start`, `Update`, `FixedUpdate`, `OnCollisionEnter`
- **Prefer `dotnet CLI`** — cross-platform, works without Visual Studio
