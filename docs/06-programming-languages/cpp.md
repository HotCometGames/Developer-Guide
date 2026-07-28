# C++

> A high-performance, statically-typed language with full control over memory and hardware — the standard for game engines and systems programming.

> **Related:** [C#](csharp.md) | [Choosing a Language](choosing-a-language.md)

---

## What Is It?

C++ is a compiled language that gives you direct control over memory, CPU, and hardware. It's the primary language for Unreal Engine, AAA game development, operating systems, embedded systems, and performance-critical applications.

## When to Use C++

| Use Case | Good Fit? |
|----------|-----------|
| Game engines (Unreal, proprietary) | Industry standard |
| Systems programming | Excellent |
| Embedded / real-time systems | Excellent |
| High-frequency trading | Excellent |
| Desktop applications | Good (Qt, wxWidgets) |
| Web backend | Rare |
| Scripting / automation | Poor |

## Key Features

### Manual Memory Management

C++ gives you full control over memory allocation and deallocation:

```cpp
int* ptr = new int(5);    // allocate on heap
delete ptr;                // free memory
ptr = nullptr;             // avoid dangling pointer
```

### RAII (Resource Acquisition Is Initialization)

Resources are tied to object lifetimes — they're acquired in the constructor and released in the destructor:

```cpp
class FileHandle {
    FILE* file;
public:
    FileHandle(const char* path) { file = fopen(path, "r"); }
    ~FileHandle() { if (file) fclose(file); }
    // Use file...
};  // Automatically closed when FileHandle goes out of scope
```

### The Standard Template Library (STL)

```cpp
#include <vector>
#include <algorithm>

std::vector<int> numbers = {3, 1, 4, 1, 5, 9, 2, 6};
std::sort(numbers.begin(), numbers.end());
auto it = std::find(numbers.begin(), numbers.end(), 5);
```

### Move Semantics (C++11)

Transfer ownership of resources without copying:

```cpp
std::vector<int> createLargeVector() {
    std::vector<int> v(1000000);
    return v;  // move — no copy overhead
}

std::vector<int> dest = std::move(source);  // source is now empty
```

### Smart Pointers (C++11)

```cpp
#include <memory>

std::unique_ptr<Player> player = std::make_unique<Player>();  // exclusive ownership
std::shared_ptr<Enemy> enemy = std::make_shared<Enemy>();     // shared ownership
std::weak_ptr<Enemy> observer = enemy;                         // non-owning reference
```

## C++ in Unreal Engine

Unreal extends C++ with a reflection system via macros:

```cpp
UCLASS()
class AMyCharacter : public ACharacter
{
    GENERATED_BODY()

public:
    UPROPERTY(EditAnywhere, BlueprintReadWrite)
    float Health = 100.0f;

    UFUNCTION(BlueprintCallable)
    void TakeDamage(float Damage);
};
```

## Common Pitfalls

| Pitfall | Why | Fix |
|---------|-----|-----|
| Undefined behavior | Accessing freed memory, buffer overflows, signed integer overflow | Use smart pointers, bounds-checked containers, enable sanitizers |
| Memory leaks | Forgetting to `delete` | Use `unique_ptr`/`shared_ptr` instead of raw pointers |
| Dangling pointers | Pointer to freed memory | Use `weak_ptr` or set to `nullptr` after `delete` |
| Header complexity | Circular includes, long compile times | Use forward declarations, precompiled headers, modules (C++20) |
| Template error messages | Cryptic, multi-line error spew | Use concepts (C++20) for better errors. Isolate template issues incrementally |
| Object slicing | Assigning derived to base by value | Use pointers or references for polymorphic types |

## Modern C++ (C++11 and later)

C++ has evolved significantly:

| Feature | Version | What It Does |
|---------|---------|-------------|
| `auto` | C++11 | Type inference |
| Smart pointers | C++11 | Automatic memory management |
| Move semantics | C++11 | Efficient resource transfer |
| Lambda expressions | C++11 | Anonymous functions |
| `constexpr` | C++11 | Compile-time evaluation |
| `if constexpr` | C++17 | Compile-time branching |
| Structured bindings | C++17 | Destructure tuples/pairs |
| Concepts | C++20 | Constrain template parameters |
| Ranges | C++20 | Composable algorithm pipelines |
| Modules | C++20 | Replace headers (experimental) |
| `std::string_view` | C++17 | Non-owning string references |

## Best Practices

- **Prefer smart pointers** over raw `new`/`delete`
- **Use RAII** for all resource management (files, locks, memory)
- **Enable compiler warnings** — `-Wall -Wextra -Wpedantic` (or `/W4` on MSVC)
- **Use sanitizers** — AddressSanitizer and UndefinedBehaviorSanitizer catch bugs at runtime
- **Prefer `const`** — const variables, const methods, const references
- **Avoid raw arrays** — use `std::vector`, `std::array`, `std::span`
- **Use namespaces** — prevent name collisions
- **Write modern C++** — C++17/20 is dramatically safer and more expressive than C++98
