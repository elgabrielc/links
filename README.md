# links

A single-page personal links site for Gabriel Casalduc, Founder of [Divergent Health](https://divergent.health/).

It presents a short, curated set of links as story chapters — the origin of a health journey, a self-diagnosis breakthrough, medical research work, and the launch of [myRadOne](https://myradone.com/).

For everything about the project — how to add or edit links, the design system, and deployment — see the **[Central Guide](CENTRAL_GUIDE.md)**, the single source of truth.

## Live site

https://elgabrielc.github.io/links/

## Structure

- `index.html` — the entire site: markup, styles, and links in one self-contained file (no build step, no dependencies).
- `signature.avif` / `signature.png` — the avatar image (AVIF preferred, PNG fallback).

## Development

Open `index.html` directly in a browser, or serve the folder with any static server:

```sh
python3 -m http.server
```

## Deployment

Deployed as a static site via GitHub Pages. Pushing to the default branch publishes to the live URL above.
