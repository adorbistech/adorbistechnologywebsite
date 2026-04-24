# Known Issues & Visual Fixes Needed

Status: as of first commit. Update this file as issues get fixed.

---

## 🔴 Fixed in this commit (verify in browser)

### 1. Navbar wordmark + cosmic mark overlap
- **Issue:** Cosmic-A mark and "adorbis" wordmark were overlapping in the nav, with menu items bleeding through the wordmark
- **Fix applied:** Removed cosmic mark `<span>` from navbar. Only wordmark remains in nav. Cosmic mark retained in footer.
- **Verify:** Open any page in browser, check that navbar shows `[adorbis wordmark]  About  Industries  eCommerce  Trust  Contact  [← Home button]`

### 2. Wordmark too small
- **Issue:** Wordmark was 20px tall — hard to read, looked weak
- **Fix applied:** Desktop wordmark now 28px, mobile 22px
- **Verify:** Wordmark should read clearly, dominate the nav brand area

---

## 🟡 Still needs attention

### 3. Discord link is channel-specific, not an invite
- **Current:** `https://discord.com/channels/1364237875918405776/1365904437385887814`
- **Problem:** Only existing server members can access. New visitors hit "access denied."
- **Fix:** Create a proper invite URL in Discord (Server Settings → Invites → Create → Never Expire → copy the `discord.gg/xxxxxxx` URL), then global find/replace in all 17 pages.

### 4. DPIIT certificate image not yet linked
- **Current:** About page references DPIIT `DIPP52616` with verify link to `startupindia.gov.in` only
- **To add:** Upload actual certificate JPG to `/assets/images/dpiit-certificate.jpg`, add "View certificate" link on About page

### 5. Brand fonts not yet sourced
- **Current:** Site uses Nunito (Google Fonts) as closest match to wordmark
- **Option:** If a licensed brand font is acquired, drop `.woff2` file into `/assets/fonts/` and update `@font-face` declaration in template

### 6. Wordmark has baked-in 3D bevel + textured background
- **Problem:** The PNG has a dark textured background baked in, plus 3D bevel effect. Fine at large sizes, looks heavy at nav size.
- **Recommendation:** Export a clean flat transparent wordmark from the original design source for crisper rendering, especially at small sizes

### 7. Wordmark contrast on dark background
- **Current:** The "ador" (silver) letters need a dark canvas to read well, the "bis" (blue) shows up fine. On the pure black nav background (#05060A), silver reads well. On some light sections (if any) it might not. Verify.

---

## 🟢 Nice-to-have improvements

### 8. Extract inline `<style>` blocks to shared CSS file
- **Current:** Each page has its own ~450 lines of inline CSS
- **Better:** Single `/assets/css/style.css` imported by all pages — one bug fix applies everywhere
- **Tradeoff:** Slower first load (extra HTTP request), but cached across pages

### 9. Generate proper favicons
- **Current:** Single favicon.png (actually cosmic-A)
- **Better:** Multi-size favicons (16×16, 32×32, 180×180 apple-touch-icon) in `/assets/images/favicons/`

### 10. Replace placeholder industries + use cases if real ones exist
- **Current:** Industries mega-page has 11 verticals × 4 use cases each — all written as illustrative patterns
- **Check:** Any of these pattern descriptions close enough to real client engagements that they could be identifiable? If yes, blur further.

### 11. Social Open Graph preview images
- **Missing:** `og:image` tags point to nothing
- **Add:** Create a 1200×630 preview card per page (can reuse same card for most pages) so LinkedIn/WhatsApp/Twitter shares look good

---

## 📝 Content checks

### 12. Review every page's "Book AI Consultation" CTA — some might feel overused
- All 17 pages have similar CTA blocks. Verify each feels appropriate for the page context.

### 13. Review pricing in eCommerce + SaaS pages
- Placeholder prices in INR and USD. Verify these match Adorbis's actual rate cards.

### 14. Review "30 years trading experience" vs "more than two decades" phrasing
- Founder page currently says "decades of market experience." Pick one consistent framing and confirm accuracy.

---

## How to report new issues

Add to this file or open a GitHub issue in the repo. Claude Code can read this file directly to pick up where we left off in future sessions.
