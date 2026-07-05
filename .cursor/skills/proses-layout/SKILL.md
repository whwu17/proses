---
name: proses-layout
description: |
  Layout and styling rules for the proses Jekyll novel site (Living Project / Dreaming Project).
  Use whenever editing `_layouts/*.html`, TOC pages, LP/DP chapter pages, corner badges, or
  "目录" / `.decor` positioning.

  Trigger on: 目录, decor, top position, LP/DP layout, toc page styling, corner badge,
  角标, novel-lp, novel-dp, GitHub Pages deploy verification for this repo.
---

# Proses layout skill

Canonical styling for this repo. When the user asks to adjust badge or TOC layout, match these values across **all** layout files — not just one page.

## Files to keep in sync

| File | Pages |
|------|-------|
| `_layouts/novel-lp.html` | LP chapters + LP TOC (`is_toc: true`) |
| `_layouts/novel-lp-toc.html` | Legacy LP TOC layout (keep aligned) |
| `_layouts/novel-dp.html` | DP chapters + DP TOC (`is_toc: true`) |
| `_layouts/novel-dp-toc.html` | Legacy DP TOC layout (keep aligned) |

## Corner badge `top` (user preference)

**Always use `top: 22.5px`** for the absolute-positioned corner label on every page type.

Do **not** revert to `38px`. If the user reports “no change”, check deployment before changing code again.

### LP TOC inline badge (`novel-lp.html`, `is_toc` branch)

```html
<div style="position:absolute;top:22.5px;left:0;height:54px;width:90px;text-indent:0;color:#444444;-webkit-text-fill-color:#444444;background:linear-gradient(-63deg, transparent 49%, #268f04 49.5%, #268f04 50.5%, transparent 51%);">目录</div>
```

### DP TOC inline badge (`novel-dp.html`, `is_toc` branch)

Same as LP, but gradient angle is **`-55deg`** (not `-63deg`).

### Chapter pages (`.decor` in `novel-lp.html` / `novel-dp.html`)

```css
.decor {
    height: 3rem;
    width: 5rem;
    position: absolute;
    top: 22.5px;
    text-indent: 0px;
}
```

Chapter markup:

```html
<div class="decor" style="background:linear-gradient(-63deg, transparent 49%, #268f04 49.5%, #268f04 50.5%, transparent 51%);">LP{{ page.index }}</div>
```

Use `-55deg` for DP chapter decor.

### Legacy TOC layouts (`novel-lp-toc.html`, `novel-dp-toc.html`)

```html
position:absolute;top:22.5px;left:0;
```

LP: `-63deg` gradient. DP: `-55deg` gradient.

## LP vs DP differences

| Property | LP | DP |
|----------|----|----|
| Gradient angle | `-63deg` | `-55deg` |
| Series title | Living Project / 不可接触的 | Dreaming Project / 可以接触的 |
| Decor prefix | `LP` | `DP` |

Shared accent color: `#268f04`.

## TOC badge size

On inline TOC badges in `novel-lp.html` / `novel-dp.html`: **90×54px** (`width:90px; height:54px`), aligned with chapter corner badge visual weight.

## Workflow after layout changes

1. Update **all four** `_layouts/*.html` files when changing shared positioning.
2. Commit and push to `main` (user prefers direct merge to main for layout tweaks).
3. Confirm GitHub Actions **Deploy Jekyll site to Pages** succeeded (build + deploy).
   - A successful build with a failed deploy leaves the live site unchanged.
   - Retry with an empty commit push if deploy fails with “Deployment failed, try again later.”
4. Verify live HTML:

```bash
curl -sL "https://whwu17.github.io/proses/lp/toc/" | rg "top:"
curl -sL "https://whwu17.github.io/proses/lp/1/" | rg "\.decor|top: 22\.5px"
```

Expect `top:22.5px` or `top: 22.5px` — not `38px`.

## Site URLs

- Base: `https://whwu17.github.io/proses`
- LP TOC: `/lp/toc/`
- DP TOC: `/dp/toc/`
- Chapters: `/lp/{n}/`, `/dp/{n}/`
