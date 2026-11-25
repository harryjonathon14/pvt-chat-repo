# Finding: Performance & Infrastructure

**Severity:** Medium  
**Category:** Performance (10% weight) — score **68/100** (lab CWV unavailable)

## Lab testing limitations (this audit)
- PageSpeed Insights API: unreachable from sandbox (multiple retries failed)
- Lighthouse/Playwright: Chromium install blocked (Playwright CDN ECONNRESET)
- CrUX field data: not retrieved
→ Score based on infrastructure + HTML weight signals only.

## Positive signals
| Signal | Evidence |
|--------|----------|
| Platform | Framer SSG — `server: Framer/010e668`, `ssg-status: optimized` |
| Edge cache | `server-timing: cache;desc="cached"` on repeat hits |
| Compression | `content-encoding: br` (brotli) |
| Protocol | HTTP/2 + `alt-svc: h3` |
| HTML weight (br) | Questions 43KB · blog 54KB · how-it-works 55KB · service-areas 60KB · homepage 67KB · portable-storage 70KB |
| Caching headers | `cache-control: public, max-age=0, must-revalidate` + strong `etag` + `last-modified` |
| Image CDN | framerusercontent with width/height params, webp on many assets |

## Risks
1. **Huge inline CSS / font-face block** in `<head>` (many families: Be Vietnam Pro, Geist, DM Sans, Inter, Plus Jakarta Sans, Open Sauce Sans…). Bloats critical HTML; may delay FCP.
2. **Third-party scripts**: GA4 `G-3XKL96Q97K`, Hotjar `3803497`, SoTellUs widget, Google Maps iframe (contact), OSM tiles (service-areas).
3. **OG image 209KB PNG** — fine for OG but not LCP; ensure hero images use modern formats + explicit dimensions (mostly OK on sampled pages).
4. **No preload/priority hints** observed for LCP hero in extracted head (may exist in Framer runtime CSS).
5. **`max-age=0, must-revalidate`** on HTML → every navigation revalidates (etag cheap, but no stale-while-revalidate).

## Recommended next steps (when lab tools available)
1. Run PSI/Lighthouse mobile+desktop on `/`, `/rates-promos`, `/service-areas/san-diego-ca`, a blog post.
2. Target: LCP < 2.5s, CLS < 0.1, INP < 200ms.
3. Trim unused @font-face; self-host subset; `font-display: swap` already set on some.
4. Defer Hotjar; consent-gate if required.
5. Consider `stale-while-revalidate` on HTML if content freshness allows.
