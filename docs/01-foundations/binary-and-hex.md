# Binary and Hex

> Base-2 and base-16 number systems — why developers need them, how to use them, and practical applications.

> **Related:** [Character Encoding](character-encoding.md) | [Data Formats](data-formats.md)

---

## What Is It?

Computers work in **binary** (base-2) — everything is a 0 or a 1. But binary numbers are long and hard for humans to read, so developers use **hexadecimal** (base-16) as a shorthand.

| System | Base | Digits | Example |
|--------|------|--------|---------|
| Decimal | 10 | 0-9 | 255 |
| Binary | 2 | 0-1 | 11111111 |
| Hexadecimal | 16 | 0-9, A-F | FF |

**Key insight:** One hex digit = 4 binary digits (a nibble). Two hex digits = 1 byte.

## Why Does It Exist?

You don't need hex to write most code, but it appears constantly:

- **Memory addresses** — shown in debuggers and error messages as hex: `0x7ffeefbff5a0`
- **Color codes** — `#FF5733` in CSS is RGB values in hex
- **Permissions** — `chmod 755` is binary permissions in octal (base-8)
- **Network protocols** — MAC addresses, IP v6 addresses
- **Hash values** — git commit hashes: `a1b2c3d`
- **Bit flags** — combining options with bitwise OR

## Mental Model

### Counting in Different Bases

```text
Decimal:   0  1  2  3  4  5  6  7  8  9  10 11 12 13 14 15
Binary:    0  1  10 11 100 101 110 111 1000 1001 1010 1011 1100 1101 1110 1111
Hex:       0  1  2  3  4  5  6  7  8  9  A   B   C   D   E   F
```

### Converting

```text
Binary → Hex:
  1101 1101  →  DD
  ^^^^ ^^^^
  D(13) D(13)

Hex → Decimal:
  1A  =  1*16 + 10  =  26
  FF  =  15*16 + 15 =  255

Decimal → Binary:
  42  =  32 + 8 + 2  =  00101010
```

### Bitwise Operations

| Operator | Symbol | Meaning | Example |
|----------|--------|---------|---------|
| AND | `&` | Both bits are 1 | `0b1100 & 0b1010 = 0b1000` |
| OR | `\|` | Either bit is 1 | `0b1100 \| 0b1010 = 0b1110` |
| XOR | `^` | Bits differ | `0b1100 ^ 0b1010 = 0b0110` |
| NOT | `~` | Flip all bits | `~0b1100 = ...11110011` (infinite leading 1s) |
| Left shift | `<<` | Shift bits left (multiply by 2) | `0b0011 << 2 = 0b1100` |
| Right shift | `>>` | Shift bits right (divide by 2) | `0b1100 >> 2 = 0b0011` |

**Practical use:** Flags and permissions.

```text
Permission flags:
  READ    = 0b100 (4)
  WRITE   = 0b010 (2)
  EXECUTE = 0b001 (1)

  READ | WRITE = 0b110 (6)  ← combined permission
  value & READ → non-zero if READ is set
```

## Cheat Sheet

```
Common powers of 2:
  2^10 = 1024     (1 KB)
  2^20 = 1,048,576 (1 MB)
  2^30 = 1,073,741,824 (1 GB)

Hex prefix: 0x  (most languages), #  (CSS)
Binary prefix: 0b (Python, JS, Rust, C#)

Quick hex-to-decimal:
  0x0-F:   0-15
  0x10:    16
  0xFF:    255
  0x100:   256
  0xFFFF:  65535

In code:
  Python:   0xFF & 0x0F  →  0x0F
  C#:       0xFF & 0x0F  →  0x0F
  JS:       0xFF & 0x0F  →  0x0F
```

## Common Mistakes

| Mistake | Problem | Solution |
|---------|---------|----------|
| Confusing decimal and hex | Expecting 10 from `0x10` | Remember: `0x10` = 16 |
| Forgetting hex prefix | Number interpreted as decimal | Use `0x` prefix for hex literals |
| Off-by-one in bit positions | Wrong flag check | Bits are 0-indexed from the right |
| Not masking after shift | Sign extension on signed types | Use `>>>` in JS, `& 0xFF` to mask |
| Ignoring endianness | Reading bytes in wrong order | Network byte order is big-endian |

## Related Topics

- [Character Encoding](character-encoding.md) — How text becomes bytes
- [Data Formats](data-formats.md) — Structured data sits on top of bytes
- [How Computers Work](how-computers-work.md) — Memory addresses and CPU operations

## Further Learning

- [Bit Twiddling Hacks](https://graphics.stanford.edu/~seander/bithacks.html) — Sean Eron Anderson
- [Hex Fiend](https://hexfiend.com/) — macOS hex editor
- [ImHex](https://imhex.werwolv.net/) — Cross-platform hex editor

---

> **Next:** [Data Formats](data-formats.md) | **Previous:** [Line Endings](line-endings.md)
