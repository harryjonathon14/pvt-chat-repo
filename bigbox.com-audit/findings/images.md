# Finding: Images

**Severity:** Low–Medium  
**Category:** Images (5% weight) — score **70/100**

## Strengths
- Content images largely **WebP** via framerusercontent CDN
- Explicit **width/height** (or query `?width=&height=`) on most `<img>` → low CLS risk
- Descriptive alts on editorial/photo assets, e.g.:
  - "A worker loads a cardboard box into a large blue Big Box storage container…"
  - "A blue Big Box Storage truck and two branded storage containers sit on a residential street…"
- Logo present (KIinXdI8YU8GTSTy9MCUFCEXyNw.webp, 1263×1245)

## Issues
1. **Sitewide og:image** — same 1200×630 PNG (209KB) on every URL; no page-specific social cards.
2. **Generic icon alts** — many UI icons as "Image 35: Icon", "Image 1…"; decorative icons should be `alt=""`.
3. **Mixed raster sizes** — some source images very large (e.g. 6240×4160 hero URL params on Pala) — CDN resizes, but ensure srcset/display sizes cover mobile.
4. **Google Maps iframe** on contact — heavy; consider static image + click-to-open.
5. No AVIF observed (webp is acceptable).

## Fix
1. Template OG images: brand + page type (+ city for service areas).
2. Audit alts: meaningful for photos, empty for decorative.
3. Confirm responsive `srcset`/`sizes` in production HTML (Framer usually handles).
4. Lazy-load below-fold embeds (OSM map on service-areas hub).
