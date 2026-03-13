# CLAUDE.md — a-css-branding

## Project Overview

`a-css-branding` is a minimal, dependency-free CSS branding/theming library. It applies a consistent dark-theme visual identity (dark background, white text, hot-pink accent) to a broad set of standard HTML elements. It is intended to be dropped into any HTML project or front-end framework as a stylesheet link.

The project has no build system, no JavaScript framework, and no package manager. It consists of two files:

- `branding.css` — the main deliverable: a complete CSS branding/reset stylesheet
- `index.html` — a redirect page that forwards visitors to `branding.css` for direct browser inspection

---

## Repository Structure

```
a-css-branding/
├── .gitattributes   # Git line-ending normalization (text=auto)
├── README.md        # Minimal project title
├── index.html       # Browser redirect to branding.css
└── branding.css     # Main CSS branding stylesheet (~303 lines)
```

---

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Styling | Plain CSS (no preprocessors) |
| Markup | HTML5 |
| Build | None — static assets only |
| Dependencies | None |
| Package manager | None |

---

## Development Workflow

There is no build step. Editing `branding.css` directly is all that is needed.

**To test changes:**
1. Open `index.html` in a browser (it redirects to `branding.css`)
2. Or link `branding.css` into an HTML file that uses a representative set of semantic elements and form controls
3. Verify the branding renders correctly across: headings, paragraphs, links, forms, media elements, lists, blockquotes, details/summary, and interactive elements

**No linters, test runners, or CI pipelines are configured.**

---

## CSS Architecture & Conventions

### CSS Custom Properties (variables)

All brand colors are defined as custom properties on `:root`. Always use these variables — never hardcode brand colors.

```css
:root {
    --c-branding-bg:     #212121;  /* Dark background */
    --c-branding-text:   white;    /* Primary text */
    --c-branding-accent: #f06;     /* Hot-pink accent */
}
```

**Naming convention:** `--c-branding-<role>` — prefix all new variables with `--c-branding-`.

### Known inconsistency to fix

The focus outline at `branding.css:194` is currently hardcoded:

```css
outline: 2px solid #007bff; /* should use var(--c-branding-accent) */
```

When touching focus styles, replace `#007bff` with `var(--c-branding-accent)`.

### Section organization

Sections are delimited with block comments. Follow the same style when adding sections:

```css
/*
 *
 * SECTION NAME
 *
 */
```

### Existing sections (in order)

1. CSS Custom Properties (`:root` variables)
2. `body` base styles
3. Typography: `article`, `p`, `q`/`cite`/`abbr`/`s`/`code`, `kbd`, `blockquote`, `hr`, `h1–h6`
4. Interactive/inline: `button`, `a`, `::selection`, `::marker`
5. Input caret (`input`, `textarea` caret-color)
6. Media elements: `img`, `picture`, `video`, `iframe`, `canvas`
7. `details` / `summary`
8. Forms reset: `fieldset`, `legend`, form inputs (`-webkit-appearance` reset)
9. Focus styles
10. Cursor styles
11. Form field sizing
12. Popover (`button.popover`, `:popover-open`)
13. Textarea specifics
14. Scrollbar (`::webkit-scrollbar*`)

### Commented-out code

The file contains intentionally commented-out rules (experimental or alternative approaches). Do not delete these without understanding their context. Add new experiments as comments rather than removing existing ones.

### Language note

Some inline comments are written in Spanish (the author's working language). This is intentional; do not "fix" them.

---

## Element Coverage

When adding new element styles, check whether the element already has rules elsewhere in the file to avoid duplication. Key elements currently styled:

- **Text/inline:** `p`, `q`, `cite`, `abbr`, `s`, `code`, `kbd`, `blockquote`, `hr`
- **Headings:** `h1`–`h6`
- **Links:** `a`, `a:hover`, `a:visited`
- **Lists/disclosure:** `::marker`, `details`, `summary`
- **Media:** `img`, `picture`, `video`, `iframe`, `canvas`
- **Forms:** `input[type=text/submit/reset/button/image/password]`, `textarea`, `select`, `button`, `label`, `fieldset`, `legend`
- **Pseudo-elements:** `::selection`, `::marker`, `::-webkit-scrollbar*`, `:popover-open`
- **Layout:** `body`, `article`, `marquee`

---

## Key Constraints & Guidelines for AI Assistants

1. **No build tools** — do not introduce npm, bundlers, preprocessors, or task runners unless explicitly requested.
2. **No new dependencies** — this project has zero dependencies; keep it that way.
3. **Variables over hardcoded values** — always use `var(--c-branding-*)` for brand colors.
4. **Minimal scope** — this is an intentionally small, focused stylesheet. Avoid scope creep.
5. **Preserve commented code** — treat commented-out blocks as documentation of considered alternatives.
6. **Static delivery** — `branding.css` is meant to be served as a raw file or linked directly; do not wrap it in a module system.
7. **Cross-browser** — include `-webkit-` prefixes where they already appear (scrollbars, appearance resets); follow the same pattern for new additions.
8. **Accessibility** — always define visible focus styles. Do not remove `outline` without replacing it with a visible alternative.

---

## Git Information

- **Primary author:** Carl Johansson
- **Initial commit:** August 17, 2025
- **Line endings:** LF (enforced by `.gitattributes`)
- **Active development branch convention:** `claude/<description>-<id>`
