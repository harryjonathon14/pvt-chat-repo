# Finding: AI Search / GEO Readiness

**Severity:** Medium  
**Category:** AI Search (10% weight) — score **72/100**

## Strengths
1. **`/llms.txt` present and high quality** — all 3 chunks read:
   - Business overview, authoritative rates link, estimator, FAQ, services, blog guide index, service-area list
   - Container facts: 8'×5'×7', ~1 room, lockable, weatherproof
   - Long-distance model, policies, phone/address
   - Clear "authoritative pricing" pointer → reduces hallucinated price risk
2. **robots.txt allows all crawlers** — no GPTBot/ClaudeBot/etc. blocks (good for citation eligibility).
3. **Stable, crawlable URL structure** — static Framer SSG HTML, fast edge cache.
4. **Real-world proof signals** — awards, SoTellUs 4.9/1496, Google reviews embed, years in business (2003).

## Gaps
| Gap | Impact |
|-----|--------|
| `llms-full.txt` → **404** | If referenced anywhere, dead end for AI agents wanting full corpus |
| JSON-LD sparse (see schema finding) | Machines prefer structured NAP/Offer/FAQ over prose |
| Contradictory facts (phone, delivery time, moving vs self-load) | LLMs may answer inconsistently or pick wrong fact |
| Soft-404 returns homepage title/description | Confuses crawlers about what failed |
| Duplicate blog/news URL | Splits citation signals |
| No author/E-E-A-T markup on blog | Weakens experience signals for YMYL-adjacent moving/storage advice |
| Geographic disambiguation | Strong San Diego focus in copy — good; ensure LocalBusiness geo + `areaServed` in schema for machine locality |

## Recommendations (GEO-specific)
1. Keep `llms.txt` updated monthly (rates, hours, phone, new areas).
2. Either fix `llms-full.txt` (concatenate full markdown corpus) or drop any links to it.
3. Make one phone number canonical everywhere (human + schema + llms.txt).
4. Add `FAQPage` + `LocalBusiness` JSON-LD so AI scrapers get fact tables, not paragraphs.
5. Resolve service-model contradiction so agents don't claim "full-service moving" incorrectly.
6. Consider `llms.txt` link in robots.txt as comment (optional convention).
