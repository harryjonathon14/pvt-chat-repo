# Finding: Security Headers Grade D

**Severity:** High  
**Category:** Technical SEO / Security  
**Evidence:** securityheaders.com scan (2026-11-25) → grade **D**

## Present
- `Strict-Transport-Security: max-age=31536000` (no preload)
- `X-Content-Type-Options: nosniff`
- HTTP/2 + `alt-svc: h3`
- Brotli content-encoding

## Missing
- `Content-Security-Policy` (and CSP-Report-Only)
- `X-Frame-Options` (or CSP `frame-ancestors`)
- `Referrer-Policy`
- `Permissions-Policy`

## Duplicated (Framer platform quirk)
- HSTS emitted twice
- `X-Content-Type-Options` emitted twice

## Impact
- Browser exploit surface (clickjacking, XSS without CSP)
- Not a direct ranking factor, but part of technical trust signals; enterprise/brand searches and some security audits flag it.

## Fix
1. In Framer **Site Settings → Custom Code / Headers**, add:
   - `Content-Security-Policy` (start report-only, then enforce; allow `framerusercontent.com`, Google Analytics, Hotjar, SoTellUs, Google Maps/OSM as needed)
   - `X-Frame-Options: SAMEORIGIN` (or CSP frame-ancestors 'self')
   - `Referrer-Policy: strict-origin-when-cross-origin`
   - `Permissions-Policy: camera=(), microphone=(), geolocation=()`
2. Deduplicate HSTS/nosniff at the edge if Framer allows; if not, document as platform limitation.
3. Add `includeSubDomains; preload` to HSTS once subdomains are inventoried.
