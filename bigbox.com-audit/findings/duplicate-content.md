# Finding: Duplicate Content — Blog vs News

**Severity:** High  
**Category:** Content / Technical  
**Evidence:** Full fetch of both URLs 2026-11-25

## Confirmed duplicate pair
| URL | Date shown | Delta |
|-----|------------|-------|
| `https://www.bigbox.com/blog/we-joined-the-bgcec-golf-day-heres-why-it-mattered` | Jul 29, 2026 | Adds FAQ section + "Summarize With AI" widget |
| `https://www.bigbox.com/news/we-joined-the-bgcec-golf-day-heres-why-it-mattered` | Jul 17, 2026 | Slightly different nav/footer chrome |

Body copy is near-identical (same BGCEC Golf Day 2026 sponsorship story, same structure). Two indexable URLs compete for the same query.

## Sitemap overlap
- ~152 `/blog/*` + ~25 `/news/*` URLs
- Slug intersection: `we-joined-the-bgcec-golf-day-heres-why-it-mattered` only (from sampled inventory), but pattern risk is structural: **same CMS often publishes to both collections**.

## Secondary duplication risks
- 47 `/service-areas/*` pages share boilerplate (hero, 4-step strip, reviews widget, contact block) — unique city paragraphs exist on sampled pages (Carlsbad, Pala, Palomar Mountain) but several claim overlapping service lists.
- Sitewide og:image identical PNG on every URL (weak for social differentiation, not classic duplicate content).

## Fix
1. Pick **one canonical home** for company news (recommend `/news` for PR, `/blog` for educational SEO) — 301 the other URL.
2. For the golf-day post: 301 blog → news (or vice versa); update sitemap to only list the surviving URL.
3. Add unique intros/outros or canonical tags if both collections must remain.
4. Audit remaining slugs programmatically for blog∩news collisions.
