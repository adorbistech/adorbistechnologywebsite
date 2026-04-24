# Deployment Guide

Deploy the Adorbis site from GitHub → Hostinger VPS via Caddy. Hostinger manages DNS; no Cloudflare.

---

## Prerequisites

- ✅ Hostinger KVM VPS (same one running Ollama)
- ✅ SSH access from Windows (PowerShell / Windows Terminal)
- ✅ GitHub repo: `https://github.com/adorbistech/adorbistechnologywebsite`
- ✅ Domain `adorbistechnology.com` — DNS panel accessible via Hostinger hPanel
- ✅ Wix Premium active (keep live until VPS is verified working)

**IMPORTANT — Do NOT disconnect from Wix until you've tested the VPS site on a subdomain first.**

---

## The plan at a glance

```
User types adorbistechnology.com
   ↓
Hostinger DNS resolves → VPS IP
   ↓
Browser connects to Hostinger VPS
   ↓
Caddy serves static HTML + auto-issues Let's Encrypt SSL
   ↓
Done
```

One vendor (Hostinger) for domain + DNS + VPS. One panel for everything.

---

## Phase 1 — Deploy to VPS (zero risk, no DNS changes)

### 1.1 SSH into the VPS

```powershell
ssh root@your-vps-ip
```

If you don't know the VPS IP: log into hPanel → VPS → your VPS → overview shows the IP.

### 1.2 Install Caddy (if not already running)

```bash
apt update
apt install -y debian-keyring debian-archive-keyring apt-transport-https curl
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/gpg.key' | gpg --dearmor -o /usr/share/keyrings/caddy-stable-archive-keyring.gpg
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/debian.deb.txt' | tee /etc/apt/sources.list.d/caddy-stable.list
apt update
apt install -y caddy
```

Verify: `caddy version`

### 1.3 Clone the repo to the VPS

```bash
mkdir -p /var/www/adorbistech
cd /var/www/adorbistech

# Option A: SSH (requires an SSH deploy key added to the GitHub repo)
git clone git@github.com:adorbistech/adorbistechnologywebsite.git .

# Option B: HTTPS with Personal Access Token (simpler if SSH key isn't set up yet)
git clone https://<YOUR_GITHUB_PAT>@github.com/adorbistech/adorbistechnologywebsite.git .
```

### 1.4 Install Caddyfile and start serving

```bash
chown -R caddy:caddy /var/www/adorbistech
chmod -R 755 /var/www/adorbistech
cp Caddyfile /etc/caddy/Caddyfile
systemctl reload caddy
```

At this point Caddy is running but the domain isn't pointed at it yet. That's intentional.

---

## Phase 2 — Subdomain test BEFORE cutover

**Why:** verify everything works on a test URL before touching the live domain. Zero risk to current traffic.

### 2.1 Confirm DNS is managed by Hostinger

Log into **hPanel → Domains → `adorbistechnology.com`**. Check the nameservers:

- **If nameservers say `ns1.dns-parking.com` / `ns2.dns-parking.com` (Hostinger's):** You're set. DNS is at Hostinger. Skip to 2.2.
- **If nameservers say `ns0.wixdns.net` / `ns1.wixdns.net` (Wix's):** You need to switch nameservers to Hostinger first.
  - In hPanel → Domains → select domain → "Change Nameservers" → pick **"Use Hostinger nameservers"**
  - Wait up to 24 hours for propagation (usually 1-4 hours)
  - **Site stays on Wix this whole time** — the existing DNS records at Wix continue serving until nameservers fully propagate to Hostinger, and Hostinger's DNS will still point at Wix's IPs initially so nothing breaks

### 2.2 Add a test subdomain A record

In **hPanel → DNS Management → Manage DNS records**, add:

- **Type:** A
- **Name:** `new`
- **Points to:** your VPS IP (e.g. `192.XX.XX.XX`)
- **TTL:** 300 (5 minutes)

### 2.3 Wait for DNS propagation

5-30 minutes typical with Hostinger DNS. Check with:

```powershell
nslookup new.adorbistechnology.com
```

You should see your VPS IP in the response.

### 2.4 Visit the subdomain

Open `https://new.adorbistechnology.com` in a browser. Caddy will:
- Automatically issue a Let's Encrypt SSL certificate (takes ~30-60 seconds on first visit)
- Serve the site

**Click through every page. Test mobile view. Verify:**
- Navbar shows only the wordmark (no overlap)
- All images load from `/assets/images/`
- Fonts load (Nunito, Instrument Serif, JetBrains Mono visible in DevTools → Network)
- All CTA buttons point to `mailto:info@adorbistech.com`
- Footer shows both entities, DPIIT badge, Discord + LinkedIn + Email icons

**Only proceed to Phase 3 if everything works.**

---

## Phase 3 — The cutover (apex domain)

Once the subdomain test passes and you're ready to flip the real domain:

### 3.1 Switch Caddy to the production config

SSH into the VPS and edit the Caddyfile:

```bash
nano /etc/caddy/Caddyfile
```

Replace the subdomain block with production. The repo's `Caddyfile` has both, with the production version commented out — uncomment it and delete the subdomain block. Or replace the entire file with:

```
adorbistechnology.com, www.adorbistechnology.com {
    root * /var/www/adorbistech/pages
    file_server
    encode gzip zstd
    try_files {path} {path}.html {path}/index.html

    # Redirect www → apex
    @www host www.adorbistechnology.com
    redir @www https://adorbistechnology.com{uri} permanent

    # Security headers
    header {
        Strict-Transport-Security "max-age=31536000; includeSubDomains; preload"
        X-Content-Type-Options "nosniff"
        X-Frame-Options "SAMEORIGIN"
        Referrer-Policy "strict-origin-when-cross-origin"
        Permissions-Policy "geolocation=(), microphone=(), camera=()"
    }

    # Cache static assets for 1 year
    @assets {
        path /assets/*
    }
    header @assets Cache-Control "public, max-age=31536000, immutable"

    log {
        output file /var/log/caddy/adorbistech-access.log
        format console
    }
}
```

Reload Caddy:
```bash
systemctl reload caddy
```

### 3.2 Flip the A records in Hostinger DNS

In **hPanel → DNS Management**:

1. Find the existing A record for `adorbistechnology.com` (currently pointing to a Wix IP like `185.230.63.x`)
2. Edit it: change **Points to** from the Wix IP → your VPS IP
3. Save
4. Same for the `www` A record (or CNAME → `adorbistechnology.com`)

### 3.3 Wait for propagation

Typically 5-30 minutes with Hostinger DNS. Verify:

```powershell
nslookup adorbistechnology.com
```

When the response shows your VPS IP, the cutover is complete.

### 3.4 Verify the live site

Visit `https://adorbistechnology.com`:
- Should load from VPS (not Wix)
- SSL should be valid (Caddy issues Let's Encrypt for apex + www automatically)
- Click every page, test mobile, verify CTAs

---

## Phase 4 — Disconnect from Wix

**Only after you've confirmed the apex domain serves from VPS globally (usually within 1 hour of cutover).**

1. Log into Wix → `manage.wix.com` → your site → **Settings → Domains**
2. Click on `adorbistechnology.com` → **Disconnect from this site**
3. The Wix site remains accessible at its default `wixsite.com` URL as an archive
4. **Keep Wix Premium active for 30 days** as a rollback safety net

---

## Phase 5 — Decommission Wix (30 days later)

After 30 days of stable VPS operation with no issues:

1. Log into Wix → cancel Wix Premium subscription
2. If the domain is **registered at Wix** (not Hostinger), **transfer it out first** before cancellation — otherwise you risk losing the domain. Check in Wix's Domains panel which entity holds the registration.
3. The Wix site may go fully offline at the `wixsite.com` URL depending on plan downgrade

---

## Ongoing updates (after deployment)

From your Windows machine with Claude Code:

```powershell
cd D:\adorbistechnology\repo

# Make edits with Claude Code
# Then commit and push
git add .
git commit -m "Update copy on about page"
git push origin main

# SSH into VPS and pull
ssh root@your-vps-ip
cd /var/www/adorbistech
git pull

# Content-only changes need no Caddy reload — Caddy reads files live
# Only reload Caddy if Caddyfile itself changed:
systemctl reload caddy
```

### Automated deploy (optional — do this later)

Once you're comfortable with the manual flow, add a GitHub Actions workflow that auto-pulls on push to `main`:

```yaml
# .github/workflows/deploy.yml
name: Deploy to VPS
on:
  push:
    branches: [main]
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: SSH and pull
        uses: appleboy/ssh-action@v1.0.0
        with:
          host: ${{ secrets.VPS_HOST }}
          username: root
          key: ${{ secrets.SSH_PRIVATE_KEY }}
          script: cd /var/www/adorbistech && git pull
```

You'd need to add two GitHub repo secrets: `VPS_HOST` (the IP) and `SSH_PRIVATE_KEY` (a deploy key). Not required for launch.

---

## Rollback plan

If anything breaks after cutover, rollback is fast:

1. In **Hostinger DNS Management**, edit the A records back:
   - `adorbistechnology.com` → `185.230.63.107` (Wix IP, from the pre-cutover record)
   - `www.adorbistechnology.com` → same
2. Propagation 5-30 min
3. Site back on Wix
4. Keep investigating VPS issues at your leisure

Because you haven't disconnected from Wix yet (Phase 4 comes AFTER the cutover works), the Wix site is still live and ready to catch the domain back immediately.

**Write down the Wix IP address BEFORE the cutover so you know what to revert to if needed.** Look at the current A record for `adorbistechnology.com` in Hostinger DNS panel before changing it and screenshot the value.

---

## Optional later: adding Cloudflare

If you later see meaningful international traffic (US / EU / SEA visitors with slow page loads), Cloudflare can be added in front of your Hostinger VPS **without disrupting anything live**:

1. Sign up at [cloudflare.com](https://cloudflare.com) (free tier)
2. Add `adorbistechnology.com` as a site
3. Cloudflare scans Hostinger DNS and imports records
4. Cloudflare gives you 2 nameservers
5. Change nameservers at Hostinger from Hostinger's defaults to Cloudflare's
6. You gain: CDN caching, DDoS protection, free analytics

This is a 20-minute setup any time you want it. Not needed for launch. Fine to wait 3-6 months post-launch to decide whether you need it.

---

## Post-deployment SEO checklist

Once the site is live on `adorbistechnology.com`:

1. **Google Search Console** — add property, verify via DNS TXT record in Hostinger DNS panel, submit sitemap
2. **Bing Webmaster Tools** — same
3. **Submit sitemap.xml** — once generated, paste into Search Console
4. **`robots.txt`** — allow all major AI crawlers (GPTBot, ClaudeBot, PerplexityBot, Google-Extended, etc.)
5. **`llms.txt`** — AI crawler index file
6. **JSON-LD structured data** — Organization + Person + Service schemas
7. **Open Graph images** — 1200×630 preview cards per page

These are separate tasks — tackle after the domain cutover is confirmed stable.
