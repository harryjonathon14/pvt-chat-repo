# Full SEO Audit — bigbox.com

**Tool:** claude-seo v2.6.2 (`seo-audit` skill)  
**Target:** https://www.bigbox.com/  
**Date:** 2026-11-25  
**Business type:** Local service — portable storage, San Diego County (SAB + hybrid facility)  
**Platform:** Framer SSG (edge), `server: Framer/010e668`  
**Method:** Inline sequential checks (no subagents). Lab CWV/Lighthouse unavailable in sandbox (Chromium/PSI blocked); findings based on HTTP/microlink/jina/html2txt/search-index evidence.

---

## Executive summary

**Weighted score: 64 / 100**

Big Box runs a technically sound Framer site with excellent crawlable static HTML, a strong `llms.txt`, a large content library (152 posts + 25 news + 47 service areas), and clear local NAP — but it is held back by **sparse structured data**, **blog/news duplicate content**, **NAP & offer contradictions** (two phone numbers, self-load vs “full-service moving,” 24–48h vs 1-week booking), **security headers grade D**, and **redirect hygiene** (307 http→https, internal links that hop through 308s, soft-404 body).

Highest ROI: ship `LocalBusiness` + `FAQPage` + `BlogPosting` schema, 301 the duplicate golf-day post, unify phone/SLA/service claims, fix soft-404 + http redirect, add missing security headers.

---

## Scorecard (claude-seo weights)

| Category | Weight | Score | Weighted |
|----------|--------|------:|---------:|
| Content quality | 23% | 74 | 17.0 |
| Technical SEO | 22% | 62 | 13.6 |
| On-page SEO | 20% | 70 | 14.0 |
| Schema / structured data | 10% | 35 | 3.5 |
| Performance (CWV*) | 10% | 68 | 6.8 |
| AI search / GEO | 10% | 72 | 7.2 |
| Images | 5% | 70 | 3.5 |
| **Total** | **100%** | | **65.6 → 64** |

\*Performance score is infrastructure-based; re-run PSI/Lighthouse when available.

---

## 1. Business & local profile

| Field | Value |
|-------|-------|
| Name | Big Box Storage |
| Address | 7077 Consolidated Way, Suite D, San Diego, CA **92121** |
| Phone (primary) | **858-244-2691** |
| Phone (secondary, conflicting) | 619-353-5653 (service-areas hub / some snippets) |
| Hours | 7 days 7:30am–5pm PST; facility access 10am–4pm (how-it-works says 3pm) |
| Google Business | cid=7027956076036550772 (~684 reviews on Maps embed) |
| Reviews | SoTellUs 4.9 ★ / 1496; Google ~684 |
| Founded | 2003 (family-run); claims 23+ years |
| Offer model | Self-load portable storage 8'×5'×7' + long-distance shipping; partner movers (Gorilla Movers) |

**Local SEO notes:** Strong physical NAP + Maps embed + service-area pages. Diluted by dual phone numbers and off-model “moving company” copy on some city pages.

---

## 2. Crawl & indexation

- **robots.txt:** Allow-all + sitemap declaration ✅  
- **sitemap.xml:** ~260 URLs (35 core / 47 areas / 152 blog / 25 news / legal) ✅ volume  
- **SSR:** Titles, meta descriptions, H1s in static HTML ✅  
- **http→https:** **307** ❌ (should be 301/308)  
- **apex→www:** 308 ✅  
- **Trailing slash:** 308 → no-slash, matches sitemap ✅  
- **Soft-404:** 404 status but homepage title/description ❌  
- **Internal redirect chains:** FAQ → `/portable-storage/rates*` → `/rates-promos`; how-it-works → `/get-your-big-box/portable-storage/` → rent.bigbox.com ❌  
- **Canonical / viewport / robots meta:** attr probes null — **confirm in View-Source** ⚠️  
- **llms.txt:** excellent ✅ · **llms-full.txt:** 404 ❌  

Details: `findings/technical-crawl-index.md`, `findings/redirects-soft404.md`

---

## 3. Technical / security headers

securityheaders.com grade **D**.

| Header | Status |
|--------|--------|
| HSTS | Present (duplicated; no preload) |
| X-Content-Type-Options | Present (duplicated) |
| CSP | **Missing** |
| X-Frame-Options | **Missing** |
| Referrer-Policy | **Missing** |
| Permissions-Policy | **Missing** |
| HTTP/2 + h3 | ✅ |

Details: `findings/security-headers.md`

---

## 4. Content quality

**Strengths**
- Unique, helpful copy on hub pages; transparent pricing ($89/12-mo, $99 m2m, $0 access fees).
- 152 blog posts + 25 news + FAQ + how-it-works + estimator → strong topical coverage.
- `llms.txt` is best-in-class among sampled AI files.
- Real reviews, awards (San Diego Reader), community content → E-E-A-T raw material.

**Defects**
1. **Duplicate:** `/blog/we-joined-the-bgcec-golf-day…` ≈ `/news/we-joined-the-bgcec-golf-day…` (dates Jul 29 vs Jul 17).  
2. **Wrong-city meta:** `/service-areas/san-diego-ca` description says **Campo, CA**.  
3. **Contradictions:** phone 858 vs 619; delivery 24–48h vs 1 week; self-load vs full-service moving/white-glove/packing on city pages; access 3pm vs 4pm; award “2020–2024 = seven years” math error.  
4. Blog `author: null` (dates OK).

Details: `findings/content-contradictions.md`, `findings/duplicate-content.md`

---

## 5. On-page SEO

| Element | Verdict |
|---------|---------|
| Titles | Unique, relevant ✅ |
| Meta descriptions | Present, unique (except city template bug) ✅ |
| H1 | Single, topically aligned ✅ (fit-text extract quirk — verify textContent) |
| Keyword stuffing | `/rates-promos` H1 run-together “GettheBest…” ⚠️ |
| OG image | 1200×630 but **sitewide identical** ⚠️ |
| Internal links to redirects | Multiple ❌ |
| Blog dates | `<time>` present ✅ · authors ❌ |

Details: `findings/onpage.md`

---

## 6. Schema / structured data — **biggest gap**

| Page | JSON-LD |
|------|---------|
| `/residential-solutions` | ✅ `Service` (+ provider → LocalBusiness @id) |
| `/`, `/questions`, `/service-areas`, sample city pages, `/portable-storage`, sample blog post | ❌ null via selector |
| `/service-areas` in Google index snippet | LocalBusiness text visible — not confirmed live ⚠️ |

**Missing:** sitewide LocalBusiness/Organization, WebSite, FAQPage, Article/BlogPosting, Breadcrumb, AggregateRating.

Details: `findings/schema.md`

---

## 7. Performance

- Framer SSG + edge cache + brotli + HTTP/2/h3 ✅  
- HTML ~43–70KB compressed — acceptable; **large inline font CSS** ⚠️  
- Third parties: GA4, Hotjar, SoTellUs, Maps, OSM ⚠️  
- **No lab CWV** (PSI/Chromium blocked) — re-test externally.

Details: `findings/performance.md`

---

## 8. AI search / GEO — **72/100**

- ✅ Rich `llms.txt`, robots allows AI crawlers, stable URLs  
- ❌ `llms-full.txt` 404, sparse JSON-LD, contradictory facts, soft-404, duplicate URL  

Details: `findings/ai-search-geo.md`

---

## 9. Images

- WebP CDN, dimensions present, good photo alts ✅  
- Sitewide OG PNG, generic icon alts, heavy Maps embed ⚠️  

Details: `findings/images.md`

---

## Priority findings (severity-ranked)

| # | Severity | Finding | Category |
|---|----------|---------|----------|
| 1 | **High** | JSON-LD almost absent (only residential-solutions Service) | Schema |
| 2 | **High** | Blog/news duplicate golf-day post | Content |
| 3 | **High** | Dual phone numbers + wrong-city meta + offer contradictions | Content/Local |
| 4 | **High** | Security headers grade D (no CSP/XFO/Referrer/Permissions) | Technical |
| 5 | **Medium** | Soft-404 body; http→https 307; internal 308 chains | Technical |
| 6 | **Medium** | Canonical/viewport unconfirmed | Technical |
| 7 | **Medium** | llms-full.txt 404; fit-text H1 risk; sitewide OG | On-page/AI |
| 8 | **Medium** | No lab CWV; inline font CSS; Hotjar | Performance |
| 9 | **Low** | Author bylines; award-year wording; access-hours unify | Content |

---

## What’s working well (keep doing)

1. Static SSR HTML with solid titles/descriptions/H1s  
2. robots + large sitemap + 308 trailing-slash policy  
3. `llms.txt` quality and AI-friendly robots  
4. Real E-E-A-T assets: reviews, awards, history, address, Maps  
5. Transparent pricing and FAQ depth  
6. Edge-cached Framer delivery with brotli/h3  

---

## Methodology limitations

- No Chromium → no screenshots/Lighthouse/visual checks  
- PageSpeed API unreachable → performance scored on signals only  
- Attr selectors for canonical/viewport returned null — may be tool limitation; **manual View-Source required** before treating as missing  
- H1 run-together strings largely extraction artifacts (html2txt/microlink show proper spaces)  

Artifacts: `audit-data.json`, `findings/*.md`.
