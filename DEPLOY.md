# Go-Live Runbook — Home Cost Calculator

Target URL: **https://calculator.innovadesignstudio.ca/**
Host: **GitHub Pages** (this repo) · Single self-contained `index.html` (fonts + images embedded).

---

## 1. Enable GitHub Pages (one time)
GitHub → this repo → **Settings → Pages**:
- **Source:** Deploy from a branch
- **Branch:** `main` (recommended — merge the launch branch first) **/ (root)**, then **Save**
- The `CNAME` file in this repo already sets the custom domain to `calculator.innovadesignstudio.ca`.
- Under **Custom domain**, confirm it shows `calculator.innovadesignstudio.ca`, then tick **Enforce HTTPS** once the cert is issued (can take a few minutes to ~1 hour).

## 2. DNS in Squarespace (one time)
Squarespace → **Settings → Domains → innovadesignstudio.ca → DNS Settings → Add record**:

| Type  | Host        | Value                     |
|-------|-------------|---------------------------|
| CNAME | `calculator`| `<your-github-username>.github.io` |

> Use the CNAME to `<user>.github.io` (NOT an A record) because it's a subdomain.
> DNS can take 15 min–48 hrs to propagate; usually fast. GitHub Pages then auto-issues the HTTPS cert.

Verify: `dig calculator.innovadesignstudio.ca +short` should return the github.io host.

## 3. Confirm the CTA target ⚠️ REQUIRED
Every button on the page opens `https://innovadesignstudio.ca/#contact-form`.
**Load your live homepage and confirm an element with `id="contact-form"` actually exists there.**
If it doesn't, either add that anchor/section on the Squarespace site, or tell me the correct URL and I'll repoint every CTA.

## 4. Lead pipe activation ⚠️ REQUIRED before ads
Leads are emailed via formsubmit.co to `alexander@` (cc `admin@`).
- Submit the form **once yourself** on the live URL.
- Check `alexander@innovadesignstudio.ca` for a formsubmit **activation email** and click the link.
- Until you do, **every lead is silently dropped.** Re-test after activating.
- Reliability note: formsubmit is a free third party and the send is fire-and-forget (a failed send still shows the visitor "success"). Consider a more robust sink before scaling spend.

## 5. Privacy policy ⚠️ (Google Ads)
Footer + lead form link to `https://innovadesignstudio.ca/privacy`.
Confirm that page exists (or give me the real URL). Google Ads lead forms need an accessible privacy policy.

## 6. Conversion tracking — Day 2 (Google Ads)
Open `index.html`, find `window.INNOVA_TRACKING` in the `<head>`, and fill the four values:
- `ga4Id` — GA4 Measurement ID (`G-…`)
- `adsId` — Google Ads tag ID (`AW-…`)
- `leadConversionLabel` — Ads conversion label for the **Lead** action
- `consultConversionLabel` — Ads conversion label for the **Book consult** action

Already wired (no code changes needed):
- **Lead form submitted** → GA4 `generate_lead` + Ads lead conversion (sends CAD estimate value)
- **"Book a consult" click** → GA4 `book_consult` + Ads consult conversion

While the values contain `XXXX`, tracking stays completely inert (nothing loads). Commit + push after filling them.

## Homepage (Day 1, second half)
"Primary CTA above the fold on homepage" is a Squarespace edit on `innovadesignstudio.ca`, not in this repo:
add a hero button linking to `https://calculator.innovadesignstudio.ca/` as the primary CTA.
