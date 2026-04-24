# Adorbis Technology — Website

Production website for **Adorbis Technology Pvt Ltd** (Hyderabad, India) and **Adorbis LLC** (Sheridan, Wyoming, USA).

Target: `https://adorbistechnology.com`

- **DPIIT Recognition:** DIPP52616 (Startup India, Govt of India)
- **Partners:** Wix Marketplace Partner, Shopify Partner
- **Contact:** info@adorbistech.com
- **Entities:** Adorbis Technology Pvt Ltd (India) + Adorbis LLC (Wyoming, USA)

---

## Quick start (Windows with Claude Code)

```powershell
# Clone
git clone git@github.com:adorbistech/adorbistechnologywebsite.git
cd adorbistechnologywebsite

# Preview locally
# Double-click _preview.html — it's a page index that links to all 17 pages
# Or serve with python's built-in server:
python -m http.server 8000
# Then open http://localhost:8000/_preview.html
```

---

## Project structure

```
adorbistechnologywebsite/
├── pages/                      # 17 HTML pages (production-ready)
│   ├── index.html              # Landing page
│   ├── about.html              # About + DPIIT + dual-entity
│   ├── founder.html            # Founder (anonymous) + LinkedIn + Discord
│   ├── clients.html            # Clients/Trust/NDA framework
│   ├── industries.html         # 11 industry verticals mega-page
│   ├── contact.html            # Contact info
│   ├── process.html            # 3-phase engagement process
│   ├── model-training.html     # AI service: Model Training
│   ├── workflow-automation.html  # AI service: Workflow Automation
│   ├── private-llms.html       # AI service: Private LLMs
│   ├── ai-infrastructure.html  # AI service: Infrastructure
│   ├── ai-enhancement.html     # AI service: Software Enhancement
│   ├── ecommerce.html          # Development: eCommerce (Wix + Shopify)
│   ├── saas.html               # Development: SaaS Applications
│   ├── docs.html               # Documentation page
│   ├── security.html           # Security & compliance
│   └── privacy.html            # Privacy policy
├── assets/
│   ├── images/
│   │   ├── adorbis-wordmark.png    # "adorbis" wordmark (silver + blue)
│   │   ├── adorbis-cosmic-a.png    # Cosmic-ringed A logo (footer mark)
│   │   └── adorbis-a-mark.png      # 3D silver + blue A mark (alternate)
│   └── fonts/                  # (placeholder — brand fonts go here later)
├── docs/
│   ├── KNOWN-ISSUES.md         # Current bugs + visual fixes needed
│   ├── DEPLOYMENT.md           # VPS + Caddy + DNS step-by-step
│   └── CONTENT-NOTES.md        # Copy / positioning context
├── Caddyfile                   # Production web server config
├── .gitignore
└── _preview.html               # Local page index (open in browser to navigate)
```

---

## Pages overview

| Section | Page | What it covers |
|---|---|---|
| **Home** | `index.html` | Hero + trust stack + capabilities + NDA promise + process + CTA |
| **About** | `about.html` | DPIIT + dual-entity + 6-year history + philosophy |
| **About** | `founder.html` | Founder (anonymous) + LinkedIn + Discord community |
| **About** | `clients.html` | NDA-first trust framework + engagement patterns |
| **Industries** | `industries.html` | 11 verticals × 4 use cases each |
| **AI Services** | `model-training.html` | Fine-tuning LLMs on proprietary data |
| **AI Services** | `workflow-automation.html` | n8n + LangGraph automation pipelines |
| **AI Services** | `private-llms.html` | Self-hosted LLM deployment |
| **AI Services** | `ai-infrastructure.html` | GPU clusters, vector DBs, observability |
| **AI Services** | `ai-enhancement.html` | Upgrade existing software with AI plugins |
| **Development** | `ecommerce.html` | AI-native eCommerce on Wix + Shopify + headless |
| **Development** | `saas.html` | Full-stack AI-native SaaS builds |
| **Company** | `process.html` | 3-phase engagement model |
| **Company** | `contact.html` | Contact info |
| **Legal** | `docs.html` | Documentation standards |
| **Legal** | `security.html` | Security & compliance posture |
| **Legal** | `privacy.html` | Privacy policy (GDPR + DPDP compliant) |

---

## Current status

✅ **Done:**
- Content for all 17 pages (NDA-first positioning, DPIIT credibility)
- Responsive mobile layout
- Wordmark integrated in navbar + footer
- Silver→blue brand gradient on CTAs
- Nunito font (matches wordmark geometry)
- All pages reference `/assets/images/` (no base64 bloat)
- Discord + LinkedIn + Email in footer

⚠️ **Known issues** (see `docs/KNOWN-ISSUES.md`):
- Navbar overlap bug was fixed by removing cosmic mark from nav — verify in browser
- Discord link is channel-specific, should be replaced with proper `discord.gg/xxx` invite
- Wordmark has baked-in 3D bevel — may look too heavy at small sizes; cleaner flat version would be better

🚧 **Pending:**
- DPIIT certificate JPG upload to `/assets/images/dpiit-certificate.jpg` + link from About page
- SEO scaffolding (`robots.txt`, `sitemap.xml`, `llms.txt`)
- JSON-LD structured data for Google
- Open Graph preview images
- VPS deployment via Caddy
- DNS cutover from Wix → VPS via Hostinger DNS panel

---

## Design system

- **Background:** `#05060A` (deep near-black)
- **Text:** `#EDEEF2` (near-white) / `#8A8FA3` (dimmed)
- **Brand gradient:** `linear-gradient(90deg, #C8CDD6 0%, #EEF2F8 45%, #4FB9FF 55%, #1A9DFF 100%)`
  - Silver → electric blue, matching the wordmark
- **Fonts:**
  - `Nunito` — body + UI (matches wordmark geometry)
  - `Instrument Serif` — display headlines
  - `JetBrains Mono` — monospace / labels
- **Core design:** Dark premium with neural-network SVG hero animation, floating orbs (blur + mix-blend-mode), fine grid overlay

---

## Deployment target

- **VPS:** Hostinger KVM (same instance as Ollama)
- **Web server:** Caddy (auto SSL via Let's Encrypt)
- **CDN:** None at launch (optional Cloudflare later if international traffic warrants it)
- **Domain:** `adorbistechnology.com` (currently on Wix, will cut over)

See `docs/DEPLOYMENT.md` for the full step-by-step.

---

## Credits

Built by Adorbis. Content + structure collaboratively produced with Claude (Anthropic). AI-native design system inspired by premium enterprise SaaS aesthetics (Linear, Vercel).

© 2026 Adorbis Technology Pvt Ltd · Adorbis LLC. All rights reserved.
