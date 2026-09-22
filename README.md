# ResyncLabs AI — Website

Static one-page business site + Privacy Policy and Terms of Service. No build step, no dependencies, no login wall.

## Design system

The site deliberately avoids common AI-generated-site patterns (per the internal "AI Website Don'ts" reference):

| Decision | Value |
| --- | --- |
| Palette | Warm paper `#FAF8F3` + deep ink `#101318` — light-first, dark used intentionally for Services/Contact/footer |
| Accent | Exactly one: deep green `#0E7B5A`. No gradients, no glows, no glassmorphism anywhere |
| Type | Sora (headings/UI) + IBM Plex Sans (body) — full scale in `styles.css` header comment |
| Services | Ledger-style rows with index numbers — no identical icon-on-top card grid |
| Emphasis | Raised panels and rules — no colored left-border cards |
| Spacing | 8 / 16 / 24 / 40 / 64 / 96 px scale only |
| Section labels | Sentence case; no all-caps labels, no floating hero badges |
| Year | Dynamic via JS (`#copyright-year`, falls back to 2026 without JS) |
| Accessibility | WCAG AA contrast (body 8.2:1, secondary 7.6:1), skip link, 44px touch targets, keyboard nav |
| SEO | Unique meta description per page, 1200×630 OG image, JSON-LD on every page (`ProfessionalService` home, `WebPage` legal) |

## "AI Website Don'ts" compliance audit

Rule-by-rule status from the internal reference (Sep 2026). Verified by grep + browser checks, not assumed.

| Rule | Status | Notes |
| --- | --- | --- |
| No blue→purple / VibeCode Purple | Pass | Palette: paper `#FAF8F3`, ink `#101318`, green `#0E7B5A` |
| Dark mode only if intentional, unique accent | Pass | Light-first; dark used deliberately on Services/Contact/footer |
| Max 1 gradient | Pass | Zero gradients (grep-verified, comments only) |
| No colored glows / colored box-shadows | Pass | Zero `box-shadow` in stylesheet |
| No glassmorphism | Pass | Zero `backdrop-filter` |
| WCAG AA contrast | Pass | Body 8.2:1, secondary 7.6:1, on-ink secondary 7.6:1 |
| No Inter as primary font | Pass | Sora + IBM Plex Sans |
| No Space Grotesk + Instrument Serif | Pass | Not used |
| No serif-italic hero gimmick | Pass | No italic accents |
| Full type scale | Pass | H1/H2/H3/body/meta documented in `styles.css` |
| No colored left-border cards | Pass | Emphasis via raised panels and rules |
| No identical icon-on-top card grid | Pass | Ledger rows, asymmetric 3-col grid |
| No badge above hero H1 | Pass | Removed in redesign |
| No numbered 1-2-3 box sequence | Pass | None — hero flow panel is a narrative transcript, not steps |
| No floating stat banner | Pass | Hero meta line carries only verifiable facts (response times, direct line) |
| No emoji nav icons | Pass | Zero emoji (grep-verified) |
| No all-caps section labels | Pass | Sentence case; no `text-transform: uppercase` anywhere |
| No unmodified shadcn/ui | N/A | No framework — hand-written CSS, custom tokens |
| Consistent 8/16/24/40/64/96 spacing | Pass | Applied to sections, cards, panels |
| No generic hero headline | Override | Headline is client-mandated, used verbatim |
| No unfalsifiable claims | Override | Service descriptions are client-mandated verbatim |
| No stock imagery | Pass | All graphics are custom-built (SVG, Pillow-generated PNG) |
| No placeholder testimonials | Pass | None used — only verifiable facts |
| No placeholder text / dead links | Pass | Only remaining placeholder is the booking URL, documented in the go-live checklist |
| Specific CTAs | Partial | "Book a Call" is client-mandated; "Get in Touch" kept as the not-ready-to-book path per client brief |
| ≥3 verifiable data points per page | Pass (home) | Response time, direct phone, real example flow |
| Favicon 32 + 192 | Pass | `favicon-32.png`, `favicon-192.png`, plus 180 apple-touch |
| Dynamic copyright year | Pass | JS `new Date().getFullYear()`, static fallback in markup |
| Mobile verified 375/390/414 | Pass | Programmatic overflow check: clean on all 3 pages × 3 widths |
| Touch targets ≥44px | Pass | Programmatic check: zero violations |
| Meta description + OG + JSON-LD | Pass | All 3 pages |
| Images WebP / lazy / width+height | Pass | No raster images in pages; PNGs are favicons/OG only, tiny and pre-sized |
| Alt text / labels / keyboard nav | Pass | All SVGs `aria-hidden`, skip link, semantic landmarks, visible focus |
| One conversion goal per page | Pass | Home: book a call. Legal: reference |
| Persuasion section order | Override | Order is client-mandated (Hero → About → Services → Contact) |
| Positioning statement | Override | Hero copy is client-mandated verbatim |

## Files

| File | Purpose |
| --- | --- |
| `index.html` | Home: hero, page launcher, CTA band |
| `about/index.html` | About page (`/about/`) |
| `services/index.html` | Services page (`/services/`) |
| `contact/index.html` | Contact page (`/contact/`) |
| `privacy/index.html` | Privacy Policy (`/privacy/`) |
| `terms/index.html` | Terms of Service (`/terms/`) |
| `styles.css` | Shared stylesheet (design tokens at top) |
| `script.js` | Dynamic year + subtle reveal (site works without JS) |
| `favicon-32.png`, `favicon-192.png`, `apple-touch-icon.png` | Brand favicons |
| `og.png` | 1200×630 social share card |

## Before you go live — 2 things to check

1. **Booking link** — `https://calendly.com/resynclabsai/30min` is a placeholder. Replace with the real Calendly URL:
   ```bash
   grep -rln "calendly.com" --include="*.html" .
   ```
2. **Domain** — canonical/OG/JSON-LD URLs assume `https://resynclabsai.com`. Stylesheet/script links are root-relative (`/styles.css`), which requires serving from the domain root (standard for Netlify/Vercel/Cloudflare Pages/GitHub Pages). For subdirectory hosting, switch to relative paths.

## Deploy

Any static host. No build command; publish the repo root. HTTPS is automatic on Netlify, Vercel, Cloudflare Pages, and GitHub Pages (Telnyx requires valid SSL).

## Telnyx Toll-Free SMS Verification checklist

- [x] HTTPS ready (valid SSL once deployed to any major static host)
- [x] No login wall — every page publicly accessible
- [x] No "under construction" placeholders — all sections fully populated
- [x] "ResyncLabs AI" prominent in header/logo on every page
- [x] Contact email on matching domain (`sana@resynclabsai.com`)
- [x] Privacy Policy and Terms of Service are real separate pages at `/privacy/` and `/terms/` (not PDFs/modals)
- [x] Mobile-responsive, fast-loading (no frameworks, ~40 KB total before font caching)
- [x] ⚠️ Exact sentence **"We will not share or sell your mobile information with third parties for promotional or marketing purposes."** — first sentence of "Mobile Information & SMS/Calling Communications" on `/privacy/`, bold in a visually distinct panel
- [x] ⚠️ Exact disclaimer **"Reply STOP to opt out. Reply HELP for help. Standard message and data rates may apply. Message frequency may vary."** — in "SMS Messaging Terms" on `/terms/`, immediately after the bold opt-in sentence, same visual treatment

## Local preview

```bash
python -m http.server 8080
# or: npx serve .
```

Then open http://localhost:8080
