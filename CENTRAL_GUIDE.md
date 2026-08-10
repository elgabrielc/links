# Central Guide (aka Gold Source)

The gold source for this project. If a fact about how this site works, how to
change it, or why it's built the way it is belongs anywhere, it belongs here.
Part wiki (what things are), part user manual (how to do things), part reference
(exact values to look up). When something changes, update this document first.

---

## 1. Overview

A single-page personal links site for Gabriel Casalduc, Founder of
[Divergent Health](https://divergent.health/). It presents a small, curated set
of links framed as story chapters — the origin of a health journey, a
self-diagnosis breakthrough, medical research work, and the launch of
[myRadOne](https://myradone.com/).

It is intentionally minimal: one hand-written HTML file, no build step, no
dependencies, no JavaScript. Everything ships as static files.

---

## 2. Quick reference

| Thing | Value |
| --- | --- |
| Live site | https://elgabrielc.github.io/links/ |
| Source of the page | `index.html` (self-contained: markup + CSS) |
| Avatar image | `signature.avif` (preferred), `signature.png` (fallback) |
| Stack | Static HTML + CSS. No JS, no build, no dependencies. |
| Fonts | Inter (body), Lora (heading) — loaded from Google Fonts |
| Deploy | GitHub Pages, publishes on push to the default branch (`main`) |
| Local preview | `python3 -m http.server`, then open `http://localhost:8000` |

---

## 3. Repository structure

```
.
├── index.html        The entire site — markup and styles in one file
├── signature.avif    Avatar image, AVIF (small, preferred)
├── signature.png     Avatar image, PNG fallback
├── README.md         Short project description + pointer to this guide
└── CENTRAL_GUIDE.md  This document
```

There is no `src/`, no bundler, and no config. The file you edit is the file
that ships.

---

## 4. Content model

The page is three parts stacked vertically inside a centered `.container`:

1. **Header** — the avatar (`.avatar`), the name (`h1`), and a subtitle
   (`.subtitle`, currently "Founder, Divergent Health").
2. **Links** — a vertical stack of link cards (`.links` > `.link`).
3. **Footer** — a single link to `divergent.health`.

### Anatomy of a link card

Each link is one `<a class="link">` containing two lines:

```html
<a class="link" href="URL" target="_blank" rel="noopener">
    <div class="link-label">Chapter title</div>
    <div class="link-title">The longer, verbatim description</div>
</a>
```

- `.link-label` — the **chapter title**. Short, in accent orange. This is the
  editorial framing (e.g. "The major breakthrough").
- `.link-title` — the **description**. Longer, dimmed. Kept verbatim / in the
  author's own words; do not paraphrase it away.
- The `→` arrow is added by CSS (`.link::after`) — do not type it into the
  markup.
- `target="_blank"` + `rel="noopener"` on every outbound link.

### Current links (in display order)

| # | Chapter title (`.link-label`) | Destination |
| --- | --- | --- |
| 1 | Origin story of the health journey | Medium: On diagnosing May-Thurner Syndrome |
| 2 | Medical research and root-causing | Claude artifact: literature-review method |
| 3 | The major breakthrough | LinkedIn: IJV compression self-diagnosis |
| 4 | Starting a company, and launching the first product | myradone.com |

> Note: the project folder is named `5-links`, but the page currently shows
> four cards. Keep this table in sync with `index.html` whenever links change.

---

## 5. User manual (how to do things)

### Add a link

1. Open `index.html`.
2. Inside `<div class="links">`, copy an existing `<a class="link">…</a>` block.
3. Set the `href`, the `.link-label` (chapter title), and the `.link-title`
   (description).
4. Place it in the position you want — cards render top-to-bottom in source
   order.
5. Update the [Current links](#current-links-in-display-order) table above.

### Edit or reorder links

- Edit the text directly in the `.link-label` / `.link-title` divs.
- To reorder, move the whole `<a class="link">…</a>` block up or down.

### Change the avatar

1. Replace `signature.avif` (and `signature.png` for the fallback) with the new
   image. Keep both filenames the same to avoid touching markup.
2. The avatar sits in a gradient circle; the image is contained at 72% and
   centered. A roughly square source works best.

### Change the name, subtitle, or footer

- Name: the `<h1>` in the header.
- Subtitle: the `<p class="subtitle">`.
- Footer link: the `<a>` inside `<footer>`.

### Preview locally

```sh
python3 -m http.server
```

Then open `http://localhost:8000`. Any static server works; the site needs no
backend.

---

## 6. Design system (reference)

All styling lives in the `<style>` block of `index.html`. The palette is
defined as CSS custom properties on `:root`.

### Colors

| Token | Hex | Used for |
| --- | --- | --- |
| `--bg` | `#14110f` | Page background (near-black, warm) |
| `--bg-elev` | `#1f1b18` | Link card background |
| `--bg-hover` | `#2a2522` | Link card background on hover |
| `--border` | `#3a322d` | Card borders |
| `--text` | `#f5f1ec` | Primary text (name, card labels) |
| `--text-dim` | `#a89e94` | Secondary text (subtitle, descriptions, arrow) |
| `--accent` | `#f08c00` | Orange — chapter titles, hover borders, links |

The avatar circle uses a gradient from `--accent` to `#b85c00`.

### Typography

| Element | Font | Weight / style | Size |
| --- | --- | --- | --- |
| `h1` (name) | Lora (serif) | 500 | 26px (22px on mobile) |
| Body / labels | Inter | 400–600 | 14–15px |
| Subtitle, descriptions | Inter | 400 | 14px |

Fonts load from Google Fonts via the `<link>` tags in `<head>` (Inter 400/500/600,
Lora 400/500 + italic). System sans-serif is the fallback stack.

### Layout

| Property | Value |
| --- | --- |
| Container max width | 520px, centered |
| Card padding | 18px 22px |
| Card radius | 14px |
| Gap between cards | 14px |
| Avatar | 96px circle (84px on mobile) |
| Mobile breakpoint | `max-width: 480px` |

### Interaction

- Cards lift slightly (`translateY(-1px)`) and gain an accent border on hover.
- The `→` arrow slides right and turns accent-colored on hover.
- All transitions are 0.15s ease.

---

## 7. Deployment

The site is served by **GitHub Pages** from this repository. Pushing to the
default branch (`main`) publishes the current files to the live URL. There is no
build or release step — the committed files are exactly what visitors receive.

To ship a change: commit it to `main` and push. Then hard-refresh the live URL
(GitHub Pages may take a short time to update, and images can be cached).

---

## 8. Editorial conventions

- **Story-chapter framing.** Each `.link-label` reads as a chapter in a
  narrative arc, not a generic label like "My Blog." Keep this voice.
- **Verbatim descriptions.** The `.link-title` text is written in the author's
  own words. Preserve it; do not "tidy" it into marketing copy.
- **Curation over completeness.** This is a short, deliberate set of links, not
  an exhaustive directory. Add sparingly.
- **No emojis** in the site content.

---

## 9. Maintenance notes

- Keep AVIF and PNG avatars in sync — the PNG is the fallback for browsers
  without AVIF support.
- Keep the [Current links](#current-links-in-display-order) table in this guide
  matched to `index.html`.
- No dependencies means nothing to update or audit — the main risk is external
  links rotting. Check them periodically.
