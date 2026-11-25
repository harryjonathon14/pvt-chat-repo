# Finding: Crawl / Indexation Fundamentals

**Severity:** Mixed (mostly good, several Medium issues)  
**Category:** Technical SEO

## What works
| Check | Result |
|-------|--------|
| robots.txt | `User-agent: *` / `Allow: /` + `Sitemap: https://www.bigbox.com/sitemap.xml` |
| sitemap.xml | Reachable; ~260 URLs: ~35 core, ~47 service-areas, ~152 blog, ~25 news, legal |
| HTTPS | Enforced (via 307 from http — see redirects) |
| Status codes | Real pages 200; unknown URLs return **404** (good) |
| Indexable content | SSR HTML — titles/descriptions/H1s present without JS |
| Duplicate host | apex → www 308 |
| Trailing slash | Normalized 308 → no-slash (matches sitemap) |

## Issues

### 1. Soft-404 content
404 status but homepage title/description reused. See `redirects-soft404.md`.

### 2. http→https uses 307 (temporary)
Should be 301/308. See `redirects-soft404.md`.

### 3. Canonical / viewport / robots-meta unconfirmed
Attr selectors returned null everywhere — verify raw HTML; add if missing.

### 4. Internal redirect chains
FAQ and how-it-works link to old paths that 308 elsewhere.

### 5. Sitemap hygiene (not fully verified)
- URL inventory looks complete vs crawled nav.
- `lastmod`/`changefreq`/`priority`: html2txt flatten — confirm presence in raw XML; if absent, consider adding `lastmod` for blog freshness.
- Ensure duplicate blog/news survivor only appears once after dedup.

### 6. Security headers grade D
See `security-headers.md`.

### 7. No `llms-full.txt`
404 while `llms.txt` exists.

### 8. Thin-risk service-area pages
47 pages; sampled ones have unique city intros but shared service boilerplate + off-model moving claims + at least one wrong-city meta (san-diego-ca → Campo).

## Quick wins
1. Fix http→https status to 301/308.
2. Fix soft-404 title/description.
3. Replace internal redirecting links.
4. Confirm canonical tags.
5. Dedup blog/news in sitemap after 301.
