# Finding: Redirects & Soft-404

**Severity:** Medium–High  
**Category:** Technical SEO

## Confirmed redirect map (microlink, 2026-11-25)

| From | To | Status | Issue |
|------|-----|--------|-------|
| `http://www.bigbox.com/` | `https://www.bigbox.com/` | **307** | Should be 301/308 (permanent). 307 = temporary → crawlers may not consolidate signals. |
| `https://bigbox.com/` (apex) | `https://www.bigbox.com/` | 308 | OK (permanent) |
| `https://www.bigbox.com/service-areas/` | `/service-areas` | 308 | Trailing-slash normalize — OK if sitemap/canonical match |
| `/portable-storage/rates-promos/` | `/rates-promos` | 308 | **Internal links still point here** (FAQ page) |
| `/portable-storage/rates` | `/rates-promos` | 308 | **Internal links still point here** |
| `/get-your-big-box/portable-storage/` | `https://rent.bigbox.com/` | 308 | External conversion path — OK but old path still linked from how-it-works |
| `/blog/<slug>/` | `/blog/<slug>` | 308 | Trailing slash normalize |

## Soft-404
- Request `https://www.bigbox.com/nonexistent-page` → **HTTP 404** but body reuses **homepage title + meta description**; final URL becomes `/404`.
- Status code is correct (404), but content signals "homepage" to users/extractors. Bad for AI crawlers that only read text.

## Internal links to redirected URLs (crawl waste)
- FAQ (`/questions`) links to `/portable-storage/rates-promos/` **and** `/portable-storage/rates` → both 308 to `/rates-promos`.
- How-it-works step 01 links to `/get-your-big-box/portable-storage/` → 308 offsite to rent.bigbox.com.

## Fix
1. Change **http→https to 301 or 308** at CDN/Framer level.
2. Update all internal links to final URLs (no redirect hops).
3. Give `/404` a real not-found title/description ("Page Not Found | Big Box Storage") and CTAs.
4. Keep 308s for trailing slashes but ensure `<link rel=canonical>` points to the no-slash form (sitemap already uses no-slash).
