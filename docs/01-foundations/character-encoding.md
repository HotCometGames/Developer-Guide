# Character Encoding

> How text is represented as bytes — ASCII, UTF-8, UTF-16, BOM, and why encoding errors happen.

> **Related:** [Line Endings](line-endings.md) | [Binary and Hex](binary-and-hex.md)

---

## What Is It?

Character encoding is the **mapping between human-readable characters and the numbers (bytes) that computers store**.

When you save text to a file, the computer has to decide:

- Which characters are available (English only? Chinese? Math symbols?)
- How many bytes each character uses (1? 2? 4?)
- How to mark the end of a file (BOM? No BOM?)

## Why Does It Exist?

Different encoding standards were created for different needs:

| Encoding | Bytes per Char | Characters | When to Use |
|----------|---------------|-----------|-------------|
| ASCII | 1 | 128 (English, numbers, basic symbols) | Legacy systems only |
| Latin-1 (ISO 8859-1) | 1 | 256 (Western European) | Legacy European text |
| UTF-8 | 1-4 | All of Unicode | **Default — use this** |
| UTF-16 | 2 or 4 | All of Unicode | Java, .NET, Windows internals |
| UTF-32 | 4 | All of Unicode | Rare (fixed-width internal use) |

**The modern rule:** Always use UTF-8 unless you have a specific reason not to.

## Mental Model

### How Encoding Works

```text
Character:    A
Unicode:      U+0041
UTF-8 Bytes:  0x41 (1 byte)

Character:    €
Unicode:      U+20AC
UTF-8 Bytes:  0xE2 0x82 0xAC (3 bytes)

Character:    𐍈
Unicode:      U+10348
UTF-8 Bytes:  0xF0 0x90 0x8D 0x88 (4 bytes)
```

### UTF-8 Encoding Structure

```text
1 byte:   0xxxxxxx                      → ASCII (0-127)
2 bytes:  110xxxxx 10xxxxxx             → Latin, Greek, Cyrillic
3 bytes:  1110xxxx 10xxxxxx 10xxxxxx    → Most other languages (CJK, emoji)
4 bytes:  11110xxx 10xxxxxx 10xxxxxx 10xxxxxx → Rare symbols
```

**Key property:** ASCII text IS valid UTF-8. A file containing only ASCII characters is identical in both encodings.

### The BOM (Byte Order Mark)

| Encoding | BOM Bytes | Used When |
|----------|-----------|-----------|
| UTF-8 | `EF BB BF` | Optional — some Windows tools add it |
| UTF-16 LE | `FF FE` | Required to distinguish LE vs BE |
| UTF-16 BE | `FE FF` | Required to distinguish LE vs BE |

**BOM problem:** The BOM is invisible in most editors but can break tools that don't expect it (especially Unix tools, shebang lines, and concatenated files).

## Common Encoding Errors

| Symptom | Likely Cause |
|---------|-------------|
| `é` shows as `Ã©` | UTF-8 bytes interpreted as Latin-1 |
| `é` shows as `©` | Latin-1 bytes interpreted as UTF-8 |
| `Invalid byte sequence` | File says UTF-8 but contains non-UTF-8 bytes |
| `UnicodeDecodeError` | Python reading UTF-8 as ASCII |
| BOM at start of file | UTF-8 file with BOM being parsed without BOM handling |
| `â€"` instead of `—` | UTF-8 em dash interpreted as Windows-1252 |

## Cheat Sheet

```
Always use UTF-8 unless you have a reason not to.

  Python: open(file, encoding="utf-8")
  Node:   fs.readFileSync(file, "utf-8")
  Git:    git config --global i18n.commitencoding utf-8

Check encoding:
  Linux/Mac:  file -I filename
  Windows:    Open in VS Code → bottom-right corner shows encoding

Convert file:
  iconv -f latin1 -t utf8 input.txt > output.txt
```

## Common Mistakes

| Mistake | Problem | Solution |
|---------|---------|----------|
| Assuming 1 byte = 1 character | Breaks on non-ASCII text like "café" or "你好" | Use UTF-8 aware string functions |
| Ignoring encoding entirely | Works in English, fails on international text | Default to UTF-8 everywhere |
| Not specifying encoding in `open()` | Default is platform-dependent | Always pass `encoding="utf-8"` explicitly |
| BOM in Unix pipelines | BOM breaks shebang, concatenation, grep | Strip BOM or use UTF-8 without BOM |
| Mixing encodings in a project | Some files UTF-8, some Latin-1 | Normalize with `iconv` or editor bulk conversion |

## Related Topics

- [Line Endings](line-endings.md) — Another invisible text format issue
- [Binary and Hex](binary-and-hex.md) — How bytes work at the lowest level
- [Data Formats](data-formats.md) — How structured text builds on encoding

## Further Learning

- [The Absolute Minimum Every Software Developer Must Know About Unicode](https://www.joelonsoftware.com/2003/10/08/the-absolute-minimum-every-software-developer-absolutely-positively-must-know-about-unicode-and-character-sets-no-excuses/) — Joel Spolsky
- [UTF-8 Everywhere](https://utf8everywhere.org/) — Manifesto and practical guide
- [What Every Programmer Absolutely Needs to Know About Encodings](https://kunststube.net/encoding/) — David C. Zentgraf

---

> **Next:** [Line Endings](line-endings.md) | **Previous:** [Environment Variables](environment-variables.md)
