# ACTION PLAN — bigbox.com

**Audit date:** 2026-11-25  
**Overall score:** 64/100  
**Strategy:** Fix trust-killers and machine-readable facts first (schema, NAP, duplicates), then redirect/header hygiene, then content polish and performance.

---

## Phase 0 — Day 1 (unblock AI & machine trust)

| # | Action | Effort | Impact | Owner hint |
|---|--------|--------|--------|------------|
| 0.1 | **Pick one canonical phone** (recommend 858-244-2691). Update every `tel:` link, footer, FAQ, llms.txt, and schema. Forward 619-353-5653 or remove. | S | High | Marketing + Dev |
| 0.2 | **Fix `/service-areas/san-diego-ca` meta description** (says “Campo, CA”). Scan all 47 area descriptions for wrong-city tokens (script: compare slug vs description). | S | High | Content |
| 0.3 | **301 the duplicate post** — choose canonical (suggest `/news/…golf-day` for PR or `/blog/…` for SEO; pick one). 301 the other; remove loser from sitemap. | S | High | Dev |
| 0.4 | **Fix soft-404** — `/404` template: title `Page Not Found | Big Box Storage`, unique description, links to rates/questions/contact. | S | Medium | Dev |
| 0.5 | **Change http→https from 307 → 301** (or 308) at CDN/Framer. | S | Medium | Dev |

## Phase 1 — Week 1 (structured data)

| # | Action | Effort | Impact |
|---|--------|--------|--------|
| 1.1 | Add **LocalBusiness JSON-LD** sitewide (or on homepage + inject on key templates): name, address 7077 Consolidated Way Suite D, 92121, tel 858-244-2691, geo, openingHours, priceRange, sameAs Google profile, `@id` consistent with residential-solutions provider. | M | **Critical** |
| 1.2 | Add **FAQPage** JSON-LD to `/questions` (and optionally FAQ sections on how-it-works / service-areas hub). | M | High |
| 1.3 | Add **BlogPosting** to all `/blog/*` + `/news/*`: headline, datePublished/dateModified, author (add visible byline), image, publisher. | M | High |
| 1.4 | Add **BreadcrumbList** to interior templates. | S | Medium |
| 1.5 | Add **WebSite** (+ optional SearchAction) on homepage. | S | Medium |
| 1.6 | Verify in View-Source: canonical, viewport, robots meta. If missing → add (canonical self; `max-image-preview:large`). | S | High |
| 1.7 | Fix or delete **`llms-full.txt` (404)**; keep `llms.txt` in sync with 0.1–0.2. | S | Medium |

## Phase 2 — Week 2 (redirects, links, headers)

| # | Action | Effort | Impact |
|---|--------|--------|--------|
| 2.1 | Replace internal links that 308: FAQ → `/rates-promos` (not `/portable-storage/rates*`); how-it-works → current conversion URL. | S | Medium |
| 2.2 | Security headers via Framer custom headers: CSP (report-only first), X-Frame-Options/frame-ancestors, Referrer-Policy, Permissions-Policy; dedupe HSTS/nosniff if possible; add `includeSubDomains` after inventory. | M | High |
| 2.3 | Confirm sitemap lists only canonical no-slash URLs; after 0.3, sitemap has one golf-day URL; consider `lastmod` on blog if Framer emits it. | S | Low |

## Phase 3 — Week 3 (content truth & E-E-A-T)

| # | Action | Effort | Impact |
|---|--------|--------|--------|
| 3.1 | **Reconcile delivery SLA** — one truth (e.g. “standard 24–48h in metro; rural/week-ahead where noted”). Update carlsbad FAQ, lincoln-acres, palomar-mountain, homepage, llms.txt. | M | High |
| 3.2 | **Rewrite off-model service-area copy** — remove “full-service moving / white-glove / packing crews” claims on city pages unless truly offered; align with self-load + partner movers. Prioritize lincoln-acres, pala, palomar-mountain; then template for all 47. | L | High |
| 3.3 | Unify **access hours** (10am–4pm vs 3pm) and **award-year sentence** (2020–2024 ≠ seven years). | S | Medium |
| 3.4 | Add **author bylines** to blog (visible + schema); strengthen About/E-E-A-T links from posts. | M | Medium |
| 3.5 | Add FAQ block + `FAQPage` on top 10 blog posts by traffic (if GSC available). | M | Medium |

## Phase 4 — Week 4 (on-page polish & performance)

| # | Action | Effort | Impact |
|---|--------|--------|--------|
| 4.1 | Rewrite `/rates-promos` H1 to natural language. | S | Low |
| 4.2 | Confirm fit-text H1 `textContent` has normal spaces; fix Framer component if not. | S | Medium |
| 4.3 | Per-template OG images (home, rates, how-it-works, each city). | M | Low |
| 4.4 | Performance: trim inline @font-face; defer Hotjar; re-run PSI mobile on 4 URLs; target LCP &lt; 2.5s. | M | Medium |
| 4.5 | Image audit: empty alt on decorative icons; lazy-load Maps/OSM embeds. | S | Low |

---

## Suggested 30-day sequence

```
Day 1:     0.1 0.2 0.3 0.4 0.5
Week 1:    1.1–1.7
Week 2:    2.1–2.3
Week 3:    3.1–3.5
Week 4:    4.1–4.5 + re-audit scores
```

## Success criteria (re-audit targets)

| Metric | Now | Target |
|--------|----:|-------:|
| Overall score | 64 | ≥ 80 |
| Schema score | 35 | ≥ 75 |
| Technical score | 62 | ≥ 78 |
| JSON-LD on homepage | none | LocalBusiness + WebSite + Breadcrumb |
| Duplicate URLs in sitemap | 1 pair | 0 |
| Phone numbers in crawl | 2 | 1 |
| Security grade | D | B+ or higher |
| llms-full.txt | 404 | 200 or removed |

## Quick-win checklist (copy/paste)

- [ ] One phone everywhere  
- [ ] Fix san-diego-ca description  
- [ ] 301 golf-day duplicate  
- [ ] Soft-404 title  
- [ ] 301 http→https  
- [ ] LocalBusiness JSON-LD  
- [ ] FAQPage on /questions  
- [ ] BlogPosting + authors  
- [ ] Fix internal 308 link hrefs  
- [ ] CSP + XFO + Referrer-Policy + Permissions-Policy  
- [ ] Confirm canonical in View-Source  
- [ ] Fix llms-full.txt  
- [ ] Unify delivery SLA + service claims  
- [ ] PSI re-test  

---

*Full evidence: `FULL-AUDIT-REPORT.md`, `audit-data.json`, `findings/*.md`.*
