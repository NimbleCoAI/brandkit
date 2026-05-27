# NimbleCo Brand Kit

Brand assets, logos, and embeddable web components for [NimbleCo](https://nimbleco.ai).

## Logo

The NimbleCo logo is a hex cluster swarm mark (S3c) paired with `{nimbleco}` in curly brackets.

| File | Use |
|------|-----|
| `logo/nimbleco-mark-dark.svg` | Swarm mark, 48px, dark backgrounds |
| `logo/nimbleco-mark-light.svg` | Swarm mark, 48px, light backgrounds |
| `logo/nimbleco-mark-dark-64.svg` | Mark at 64px |
| `logo/nimbleco-mark-dark-128.svg` | Mark at 128px |
| `logo/nimbleco-full-dark.svg` | Full lockup: mark + `{nimbleco}`, dark |
| `logo/nimbleco-full-light.svg` | Full lockup: mark + `{nimbleco}`, light |
| `logo/nimbleco-favicon.svg` | Favicon (32px, fattened for readability) |

### Colors

| Token | Dark BG | Light BG | Role |
|-------|---------|----------|------|
| Cyan | `#00dcd2` | `#00a8a0` | Primary accent, brackets |
| Magenta | `#c050d0` | `#a040b0` | Secondary accent, "co" |
| Background | `#0a0a0c` | `#f5f2ed` | Page background |

## Embeddable Components

Interactive HTML components for embedding on nimbleco.ai or anywhere via iframe.

**GitHub Pages URL:** `https://nimblecoai.github.io/brandkit/embeds/<file>`

| File | Description |
|------|-------------|
| `embeds/fluid-sim.html` | ASCII fluid dynamics hero — interactive, touch-enabled, NimbleCo palette |
| `embeds/architecture-diagram.html` | HSM architecture diagram — layered stack visualization |

### Embedding in Squarespace

**Option A — iframe (recommended for dynamic updates):**
```html
<iframe src="https://nimblecoai.github.io/brandkit/embeds/fluid-sim.html"
  style="width:100%;height:80vh;border:none;" loading="lazy"></iframe>
```

**Option B — Code Block (self-contained):**
Copy the contents of the embed file into a Squarespace Code Block.

## Blog Assets

Draft content for the MT Hermes release announcement.

| File | Description |
|------|-------------|
| `blog-assets/2026-05-27-multiplayer-agentic-ai-is-finally-here.md` | Blog post |
| `blog-assets/2026-05-27-social-thread.md` | Twitter thread + Discord post |

## License

Brand assets are copyright NimbleCo. Embeddable components are AGPL v3.
