# HTML & CSS

> The foundational languages of the web: HTML provides structure, CSS provides presentation.

> **Related:** [JavaScript](javascript.md) | [TypeScript](typescript.md)

---

## What Is It?

HTML (HyperText Markup Language) defines the structure and content of web pages. CSS (Cascading Style Sheets) controls how that content looks — layout, colors, fonts, animations.

## HTML Fundamentals

### Document Structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Page</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <header>
        <h1>Welcome</h1>
    </header>
    <main>
        <p>Hello, world!</p>
    </main>
    <footer>
        <p>&copy; 2026</p>
    </footer>
</body>
</html>
```

### Semantic Elements

Use semantic tags for accessibility and SEO:

| Tag | Purpose |
|-----|---------|
| `<header>` | Page or section header |
| `<nav>` | Navigation links |
| `<main>` | Primary content (one per page) |
| `<article>` | Self-contained content |
| `<section>` | Thematic group of content |
| `<aside>` | Sidebar or tangential content |
| `<footer>` | Page or section footer |
| `<figure>` / `<figcaption>` | Images with captions |

### Common Elements

```html
<h1> to <h6>     <!-- Headings -->
<p>               <!-- Paragraph -->
<a href="url">    <!-- Link -->
<img src="url" alt="text">  <!-- Image -->
<ul>/<ol>/<li>    <!-- Lists -->
<table>/<tr>/<td> <!-- Tables -->
<form>/<input>/<button>  <!-- Forms -->
<div>/<span>      <!-- Generic containers (div = block, span = inline) -->
```

## CSS Fundamentals

### Selectors

```css
/* Element selector */
p { color: blue; }

/* Class selector */
.highlight { background: yellow; }

/* ID selector */
#header { font-size: 24px; }

/* Descendant */
article p { line-height: 1.6; }

/* Pseudo-classes */
button:hover { background: darkgray; }
input:focus { border-color: blue; }
```

### Box Model

Every element is a box:

```
┌──────────────────────────┐
│        margin            │
│  ┌────────────────────┐  │
│  │      border        │  │
│  │  ┌──────────────┐  │  │
│  │  │   padding    │  │  │
│  │  │ ┌──────────┐ │  │  │
│  │  │ │ content  │ │  │  │
│  │  │ └──────────┘ │  │  │
│  │  └──────────────┘  │  │
│  └────────────────────┘  │
└──────────────────────────┘
```

```css
.box {
    width: 300px;
    padding: 16px;
    border: 2px solid black;
    margin: 8px;
    box-sizing: border-box;  /* width includes padding + border */
}
```

### Layout Methods

**Flexbox** — one-dimensional layout (row or column):

```css
.container {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 16px;
}
```

**Grid** — two-dimensional layout:

```css
.grid {
    display: grid;
    grid-template-columns: 1fr 2fr 1fr;
    gap: 16px;
}
```

| Method | Best For |
|--------|----------|
| Flexbox | Navigation bars, centering, card rows |
| Grid | Page layouts, dashboards, galleries |
| Float | Wrapping text around images (legacy) |
| Position | Overlays, modals, absolute positioning |

## Responsive Design

```css
/* Mobile-first approach */
.container {
    display: grid;
    grid-template-columns: 1fr;
}

@media (min-width: 768px) {
    .container {
        grid-template-columns: 1fr 1fr;
    }
}

@media (min-width: 1024px) {
    .container {
        grid-template-columns: 1fr 2fr 1fr;
    }
}
```

## CSS Preprocessors

| Tool | What It Adds |
|------|-------------|
| **Sass/SCSS** | Variables, nesting, mixins, functions |
| **PostCSS** | Plugins for future CSS features, autoprefixing |
| **Tailwind CSS** | Utility-first framework (not a preprocessor) |

## Common Pitfalls

| Pitfall | Why | Fix |
|---------|-----|-----|
| Specificity wars | Overly specific selectors require `!important` | Use BEM naming or utility classes. Avoid `!important` |
| Missing `box-sizing: border-box` | Width doesn't include padding/border | Apply globally: `*, *::before, *::after { box-sizing: border-box; }` |
| Not using semantic HTML | Bad accessibility and SEO | Use `<nav>`, `<main>`, `<article>` instead of `<div>` |
| Inline styles | Hard to override, no media queries | Use classes and external CSS |
| Over-nesting in SCSS | Generates overly specific selectors | Limit nesting to 3 levels max |
| No alt text on images | Accessibility failure | Always add descriptive alt text |

## Best Practices

- **Use semantic HTML** — accessibility and SEO start with correct markup
- **Mobile-first CSS** — base styles for mobile, `@media` for larger screens
- **Use a CSS reset** — normalize browser defaults (`box-sizing`, margins, fonts)
- **Keep CSS DRY** — reuse classes, avoid repeating properties
- **Learn DevTools** — inspect elements, tweak CSS live, debug layouts
- **Optimize images** — use appropriate formats (WebP, AVIF) and sizes
- **Use flexbox and grid** — avoid older layout hacks (floats for layout)
