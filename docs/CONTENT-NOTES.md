# Content & Positioning Notes

Context for anyone (human or Claude Code) making future edits to the site.

---

## Core positioning

**"AI infrastructure company that keeps your data behind your walls."**

Adorbis does three things, equally important:
1. **AI infrastructure** — model training, private LLM deployment, workflow automation, AI-native SaaS builds
2. **eCommerce** — Wix + Shopify + headless stores with AI content/imagery/automation baked in
3. **AI software enhancement** — upgrading existing enterprise software with AI plugins rather than replacing it

Every service is delivered **under mutual NDA** — no client names are ever published.

---

## Trust stack (what makes Adorbis credible)

Used on the landing page and throughout. In priority order:

1. **DPIIT Recognition** (DIPP52616) — Govt of India startup recognition, verifiable on startupindia.gov.in
2. **Dual-entity** — Adorbis Technology Pvt Ltd (Hyderabad) + Adorbis LLC (Sheridan, Wyoming) — clean contracting on both continents
3. **Since 2019** — 6+ years of shipping production software
4. **NDA-first** — every engagement begins under mutual NDA
5. **Wix Marketplace Partner** + **Shopify Partner**
6. **LinkedIn + Discord** community

---

## What we don't say

- **No named clients.** Ever. Not even anonymized in a way that's identifiable. NDA is absolute.
- **No fake testimonials.** We've burned the Priya Nair / Markus Feld / Anya Brandt quotes that were in the original design file. Any future testimonials must be real with written consent.
- **No big-tech alumni claims.** Honest positioning: "we're not ex-Google, we're builders who ship."
- **No hourly billing.** Every engagement is fixed scope, fixed price.

---

## Voice

- **Direct.** Short sentences. Strong verbs. Minimal hedging.
- **Confident but honest.** If we can't do something, we say so (see the "What we don't build" sections on saas.html and ai-enhancement.html).
- **Technical when appropriate.** Specific tool names (Ollama, vLLM, LangGraph, Nunito, oklch) signal real practice. Generic "AI solutions" signals marketing fluff.
- **Lowercase intensity.** The wordmark is lowercase. The voice is confident-lowercase, not SHOUTING.

---

## Pricing conventions (currently in eCommerce + SaaS pages)

Displayed in **INR (₹) with USD in parentheses** for international buyers.

Current placeholders (verify these match real Adorbis rate cards):
- eCommerce basic builds: ₹1.5-3 lakh (USD 1,800-3,600)
- eCommerce complex/multi-vendor: ₹8-20 lakh+ (USD 10K-25K+)
- SaaS MVP builds: ₹12-30 lakh (USD 15K-36K)
- SaaS embedded retainer: ₹8-25 lakh/month (USD 10K-30K/month)

---

## Industries covered (11 verticals on industries.html)

1. Finance & Banking
2. Retail & eCommerce
3. Transport & Logistics
4. Medical Research
5. Education Technology
6. Hospitals & Clinics
7. Schools & K-12
8. Chartered Accountants & CPAs
9. Architecture & Design Firms
10. Manufacturing Industries
11. Factories & Plant Operations

Each has an icon, tagline, intro, 6 pain-point tags, 4 concrete use cases. The framing is "capability patterns" not "shipped to X clients in this vertical."

---

## Founder page

Intentionally **anonymous**. References:
- "The founder" / "CEO & Co-founder" (no name)
- LinkedIn link (which does name Syed Suhail Dastgir — this is fine, LinkedIn is his personal public profile)
- Discord community
- Email

**Do not** add the founder's name to the page body. Prospects who want it can click to LinkedIn.

---

## Locations

**Headquarters (India):**
Adorbis Technology Pvt Ltd
1st floor, Hitech City Rd
Kondapur, Hyderabad — 500084
Telangana, India

**US entity:**
Adorbis LLC
Sheridan, Wyoming, USA

**Contact:**
- Email: info@adorbistech.com
- Phone: +91 63016 44963
- Hours: Mon-Fri 11am-6pm IST, Sat 11:30am-4pm IST

---

## Design tokens (CSS)

See any page's `<style>` block. Key values:

```css
--bg: #05060A;                /* Near-black background */
--ink: #EDEEF2;               /* Near-white primary text */
--ink-dim: #8A8FA3;           /* Dimmed secondary text */
--adorbis-silver: #C8CDD6;    /* "ador" silver */
--adorbis-silver-hi: #EEF2F8; /* Silver highlight */
--adorbis-blue: #1A9DFF;      /* "bis" blue */
--adorbis-blue-hi: #4FB9FF;   /* Blue highlight */
--adorbis-grad: linear-gradient(90deg, #C8CDD6 0%, #EEF2F8 45%, #4FB9FF 55%, #1A9DFF 100%);

--sans: 'Nunito', system-ui, sans-serif;           /* Body + UI */
--serif: 'Instrument Serif', Times, serif;         /* Display headlines */
--mono: 'JetBrains Mono', ui-monospace, monospace; /* Code, labels */
```

---

## Key URLs

- Production: `https://adorbistechnology.com` (after cutover)
- Subdomain test: `https://new.adorbistechnology.com` (during deployment)
- LinkedIn (founder): `https://www.linkedin.com/in/syed-suhail-dastgir-a216633b/`
- Discord community: (channel-specific URL currently — replace with proper `discord.gg/xxx` invite)
- Email CTA target: `mailto:info@adorbistech.com`

---

## When editing content

- **Global CTA email:** only ever `info@adorbistech.com`. No other address.
- **Back-to-home links:** always `https://adorbistechnology.com` (no trailing path).
- **Year:** currently 2026 (in copyright footers). Update annually.
- **Every page** should have: nav, main content, footer. Do not delete nav or footer.
- **Mobile:** test any CSS change at 420px and 720px breakpoints. Don't break the hamburger menu.
- **NDA messaging:** if adding new content, check it doesn't accidentally name a client or make specific claims beyond what's defensible.
