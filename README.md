# Craig Creative — Marketing Site

The Craig Creative consulting practice marketing site. Single static page, no build step required, deploys to any static host in under 10 minutes.

---

## TL;DR — Get live in 10 minutes

1. **Get a Web3Forms key** (2 min) → https://web3forms.com → enter your email → get a free access key emailed to you
2. **Edit `index.html`** (3 min) → swap 4 placeholders (see [Configuration](#configuration) below)
3. **Deploy to Cloudflare Pages** (5 min) → drag-drop the folder → connect domain → done

---

## Configuration

Open `index.html` and search for these strings, replacing each:

### ✓ 1. Web3Forms key — DONE

The contact form is already wired up with your Web3Forms access key. Submissions will be emailed to the address you registered with Web3Forms.

If you ever need to rotate the key: get a new one at https://web3forms.com, then search `index.html` for the old key value and replace.

### ✓ 2. Email — DONE

`alex@craig-creative.ai` is configured via Cloudflare DNS routing to Google Workspace. Email links in the site work as-is — no further changes needed.

If you ever want to add additional aliases (`hello@`, `info@`, etc.), you can configure them in Google Workspace admin or as Cloudflare Email Routing aliases.

### ✓ 3. Calendly — DONE

Wired in: `https://calendly.com/alex-craig-creative/30min`

Direct link to your 30-minute Discovery Call event. The site copy is also set to "Free 30-min" to match. If you ever rename the event in Calendly or change the duration, you'll need to update both the URL and the "30-min" text references in `index.html`.

### 4. Open Graph image (optional, can defer)

Find the line: `<meta property="og:image" content="https://craig-creative.ai/og-image.png">`

- Create a 1200×630 PNG of your site preview (Figma/Canva works great)
- Should include: Craig Creative wordmark + tagline "Software made with you, not at you"
- Save as `og-image.png` in this folder
- Once deployed, the URL `/og-image.png` will be served

You can skip this for launch — your link previews will just show the title and description without an image until you add it.

---

## Deployment options

### Option 1 — Cloudflare Pages ⭐ recommended

**Why:** Best free tier (unlimited requests, 500 builds/month), fastest CDN, free SSL, free analytics, easiest custom domain setup if you also bought your domain through Cloudflare.

1. Go to https://dash.cloudflare.com → Workers & Pages → Create → Pages
2. Choose "Upload assets" (or connect to GitHub if you've set up a repo)
3. Project name: `craig-creative`
4. Drag the entire deploy folder onto the upload area
5. Click Deploy → wait ~30 seconds → site live at `https://craig-creative.pages.dev`
6. **Custom domain:**
   - Click "Custom domains" → "Set up a custom domain"
   - Enter `craig-creative.ai`
   - If domain is on Cloudflare: instant DNS (1 click)
   - If domain is elsewhere: Cloudflare gives you DNS records to add at your registrar
   - SSL provisions automatically within ~2 minutes

### Option 2 — GitHub Pages

**Why:** If you want git version control, free hosting on github.io, very simple if you're already in GitHub workflow.

1. Create a new public repo: `craig-creative`
2. Upload all files from this folder (drag-drop in GitHub web UI works fine)
3. Settings → Pages → Source: "Deploy from a branch" → main → / (root) → Save
4. Wait 2 min — site live at `https://YOURUSERNAME.github.io/craig-creative/`
5. **Custom domain:**
   - Settings → Pages → Custom domain → enter `craig-creative.ai` → Save
   - At your domain registrar, add these DNS A records pointing to GitHub:
     - `185.199.108.153`
     - `185.199.109.153`
     - `185.199.110.153`
     - `185.199.111.153`
   - Add CNAME record: `www` → `YOURUSERNAME.github.io`
   - Wait 10 min for DNS, then check "Enforce HTTPS" in GitHub settings

### Option 3 — Netlify

**Why:** Easiest drag-and-drop deploy, great free tier, instant deploys.

1. Go to https://app.netlify.com
2. Drag the entire deploy folder onto the dashboard
3. Site is live in 30 seconds at `https://random-name.netlify.app`
4. Site settings → Change site name → `craig-creative`
5. Domain settings → Add custom domain → `craig-creative.ai` → follow DNS instructions

---

## Domain registration

You've already registered `craig-creative.ai` through Cloudflare ✓ — skip ahead to the deployment options.

For reference (in case you want a `.com` or other variant later):

| Registrar | .ai price/yr | .io price/yr | Recommended? |
|-----------|--------------|--------------|---------------|
| Cloudflare Registrar | ~$70 | ~$10 | ⭐ Yes — at-cost pricing, no upcharge |
| Porkbun | ~$70 | ~$11 | ⭐ Yes — clean UI, good support |
| Namecheap | ~$80 | ~$13 | OK |
| GoDaddy | ~$100+ | ~$25+ | No — overpriced, upsell-heavy |

---

## File structure

```
craig-creative-deploy/
├── index.html          ← The site (single file, all CSS/JS inline)
├── favicon.svg         ← Concentric Cs brand mark as favicon
├── robots.txt          ← Allows search engine crawling
├── sitemap.xml         ← Helps search engines index the site
├── _headers            ← Cloudflare/Netlify security headers
├── .gitignore          ← Standard ignores for git
└── README.md           ← This file
```

---

## Post-launch checklist

After your site is live:

- [ ] Test the contact form by submitting a real entry — check that the email reaches you
- [ ] Test the Calendly link — verify it opens to your booking page
- [ ] Test in iOS Safari (in-app browsers are a known weak spot — open from a LinkedIn DM to yourself to test)
- [ ] Test on Android Chrome
- [ ] Submit to Google Search Console: https://search.google.com/search-console (verify ownership via DNS or HTML file)
- [ ] Add Cloudflare Web Analytics or Plausible (privacy-respecting, free for small sites)
- [ ] Update LinkedIn profile URL/website field to point to craig-creative.ai
- [ ] Pin your launch post to your LinkedIn profile

---

## Updating the site later

Static HTML — to edit:

1. Open `index.html` in any text editor (VS Code, Sublime, even TextEdit)
2. Find the section you want to change
3. Save the file
4. Re-upload to your host (Cloudflare Pages auto-deploys if connected to GitHub)

Common updates you'll likely make:

- **Add a real testimonial** once you have one — add a `.testimonial` block in the about or co-creation section
- **Update pricing** when you raise rates (search for `$125` and `$150` for hourly, `$750` and `$1,200` for Discovery)
- **Add a new case study** — copy the AIex `.case-card` block and adapt for the new project
- **Adjust the "Now booking 1–2 spots" pulse pill** when you're at capacity (search for "Now booking")

---

## Tech notes

- **No build step.** Single HTML file with inline CSS and JS. Edit and deploy.
- **No JavaScript framework.** Vanilla JS for animations and form handling. ~50 lines total.
- **No tracking by default.** Add Plausible/Cloudflare Analytics if you want stats.
- **Fonts:** Bricolage Grotesque (wordmark), Fraunces (headlines), Inter (body), JetBrains Mono (code tags). All loaded from Google Fonts.
- **Form backend:** Web3Forms — no server needed. Submissions emailed directly.
- **Mobile-first:** Responsive breakpoints at 1024px and 640px.
- **Accessibility:** Forced light color scheme to prevent in-app browser dark mode issues. ARIA labels on the logo SVG. Semantic HTML throughout.

---

## Questions or issues

If something's broken on the live site:

1. Check the browser console (right-click → Inspect → Console) for errors
2. Test in an incognito/private window to rule out cache issues
3. Check that all 4 placeholders are properly replaced
4. For form submission failures — verify the Web3Forms access key is correct

Built with care. Ship it. 🚀
