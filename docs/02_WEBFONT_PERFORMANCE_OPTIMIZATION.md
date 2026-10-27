# ⚡ Web Font Performance & WOFF2 Optimization Guide

How to deliver ultra-fast typography on modern websites without layout shifts (CLS) or slow Largest Contentful Paint (LCP).

---

## 📦 1. Converting TTF/OTF to WOFF2
WOFF2 provides **up to 50% better compression** than original TTF/OTF files with Brotli compression built into the font container.

```bash
# Using google/woff2
woff2_compress my-font.ttf

# Using npm ttf2woff2
npx ttf2woff2 my-font.ttf my-font.woff2
```

---

## 🎨 2. Production `@font-face` CSS

```css
@font-face {
  font-family: 'Inter';
  font-style: normal;
  font-weight: 400 900;
  font-display: swap; /* Eliminates Flash of Invisible Text (FOIT) */
  src: url('/fonts/inter-variable.woff2') format('woff2');
  unicode-range: U+0000-00FF, U+0131, U+0152-0153; /* Preload Latin only */
}

@font-face {
  font-family: 'Kalpurush';
  font-style: normal;
  font-weight: 400;
  font-display: swap;
  src: url('/fonts/kalpurush.woff2') format('woff2');
  unicode-range: U+0980-09FF; /* Preload Bengali only */
}
```

---

## 🚀 3. HTML Preload for LCP Font
Always preload your hero headline font in the `<head>`:
```html
<link rel="preload" href="/fonts/inter-variable.woff2" as="font" type="font/woff2" crossorigin>
```

Maintained by **[Mohammad Golamrabbii](https://linktr.ee/golamrabbii)**.
