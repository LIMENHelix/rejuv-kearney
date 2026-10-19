# Rejuv Men's Health + Wellness — Kearney landing page

Temporary soft-launch lead-capture site for **Rejuv Men's Health + Wellness**, 645 State Rte 92, Kearney, MO 64060.

**Live URL:** https://limenhelix.github.io/rejuv-kearney/

**Status:** Live on GitHub Pages (public repo, `main` branch, root). Soft-launch `noindex` is active. FormSubmit activation is the remaining one-time step.

This is a single static page. No build step, no framework, no server. It can be hosted on GitHub Pages, Netlify, Vercel, or any static host.

---

## What is on the page

- Lion hero + "Stop guessing. Start measuring." positioning
- Founding 100 offer (21+ bourbon thank-you, with terms)
- Service menu: testosterone/hormone care, medical weight loss (branded tirzepatide only), ED/sexual health, full-body labs, muscle/performance, longevity, PRP, and a peptides **interest list** (not a launch service)
- Telehealth coaching: testosterone, weight loss, longevity, lifestyle/accountability, men supporting men
- Audience sections: first responders, military/veterans, divorced dads, dads/families, high performers, men 35+
- The 645 Club events: father/son, father/daughter, 3v3 basketball, group workouts, men's trips, watch/speaker nights
- Three-step first-visit flow + what to bring
- FAQ with pricing, privacy, prescriptions, telehealth, bourbon, peptides, ages
- Performance Partner section with a partner inquiry form
- Main lead form with interest pills, Zoom/in-person preference, consent, UTM/fbclid capture
- Privacy note, offer terms, medical disclaimers, 988/911 crisis language
- Sticky mobile callback + book bar
- `noindex` soft-launch tag (remove when ready for search traffic)

---

## Before you spend money on ads — confirm these

These are the assumptions baked into the page. They are easy to change.

1. **Contact routing is form-only and recipient details are not displayed.** The public page shows no phone number and no email address. The forms deliver to **Ashley as the primary recipient** and **Tracy as a hidden CC**; the addresses live in the form's hidden configuration, encoded so they do not render as plain addresses. For true source-level privacy, put the form behind a server-side relay or use FormSubmit privacy aliases.
2. **"Free 15-minute consult" and "lab panels from $100."** These came from the partnership model. Confirm with the clinical team before running ads. If the consult is not free, change the hero, header, FAQ, and form heading.
3. **FormSubmit needs one-time activation for the recipients.** The **first submission** triggers the activation email. Ashley and Tracy should click the activation link before ads run, or the first lead may not be delivered. Submit a clearly labeled test lead after publishing.
4. **Bourbon offer needs a compliance look.** It is written as 21+, while supplies last, no purchase necessary, ID required at pickup, pickup offsite, not served at the clinic. Have counsel or the clinic's compliance lead review Missouri alcohol-promotion rules before paid promotion. Meta may also restrict alcohol creative; keep ad creative focused on the consult.
5. **Peptides are not advertised as available.** Your planning sheet says peptides are gated on FDA listings and counsel approval. The page collects interest instead. If they are approved, change the card and the FAQ.
6. **Branded GLP-1 only.** The page says branded tirzepatide (Zepbound®/Mounjaro®), never compounded. Keep that language unless the clinical team changes the formulary.
7. **No medical claims or guarantees.** The page says prescriptions require a provider evaluation and not all patients qualify. Keep it that way.
8. **Meta Pixel is not installed.** A ready-to-paste snippet is commented out at the bottom of `index.html`. Replace `YOUR_PIXEL_ID` and uncomment it. The page fires `Lead` on form success. UTM and `fbclid` values are already captured into hidden form fields.

---

## How lead capture works

Both forms post to FormSubmit:

- `#leadForm` — consult request
- `#partnerForm` — partner inquiry

On submit, JavaScript:

1. Validates required fields and the phone number (optional partner phone is allowed to be blank).
2. Builds an interest summary.
3. Sets `_replyto` to the lead's email and a descriptive `_subject`.
4. Sends the form via `fetch` to the FormSubmit AJAX endpoint.
5. Shows the inline success panel and fires `Lead` (or the partner equivalent) if analytics is present.
6. If the request fails, shows a plain retry message instead of a dead end.

The forms also work without JavaScript: they post normally to FormSubmit and redirect back to `?sent=1#book` or `?partner=sent#partners`.

**Privacy:** The form asks for contact info and general interests only. It explicitly tells people not to submit medical details. Do not add free-text symptom fields without a HIPAA review and a BAA with the form processor.

---

## Publishing

The site is already a git repo. To redeploy after edits:

```bash
cd rejuv-kearney
git add .
git commit -m "Update landing page"
git push origin main
```

GitHub Pages serves `main` from the repository root. The live URL is:

`https://limenhelix.github.io/rejuv-kearney/`

If you move to a custom domain (e.g. `rejuvkearney.com`), add a `CNAME` file and update the canonical/OG URLs near the top of `index.html`.

### Remove the soft-launch noindex

Near the top of `index.html`:

```html
<meta name="robots" content="noindex, nofollow">
```

Delete that line when you want Google to index the page. Facebook link previews do not depend on it.

---

## Editing the page

Everything is in `index.html`: markup, CSS, and JavaScript. There is no build step.

- Colors: the `:root` block at the top of `<style>`.
- Type: Raleway (headings), PT Sans (body), Bai Jamjuree (UI/eyebrows).
- Images: `assets/lions-bg.jpg` (hero), `assets/og-image.jpg` (social share), `assets/favicon.png`, `assets/apple-touch-icon.png`.
- Phone/email: none are displayed. The form is the public contact path.
- Form recipients: primary in the two `<form action="https://formsubmit.co/...">` attributes; the CC is the hidden `_cc` input. Both are entity-encoded so they do not render as plain addresses.
- Interest values: the `data-interest` attributes on service cards and the checkbox values must match exactly.
- The "Founding 100" copy and terms: search for `Founding 100` and `Offer terms`.

---

## Design / brand notes

- Palette: deep slate/ink, gold `#C5A359` / `#B09243`, cream `#EFEBE1`, terracotta accent used sparingly.
- The lion image and brand system come from the existing ReJuv partnership page and the Heartland Men's Health brand spec.
- The page is intentionally a premium private-clinic look, not a generic medical-blue template.
- All content is static; there are no third-party scripts except Google Fonts (and the optional Meta Pixel once you add it).

---

## Validation performed

- 15/15 automated checks passed at desktop (1440px) and mobile (390px):
  - no broken images, no console errors
  - no horizontal overflow
  - hero image applied
  - service card preselects the matching interest and scrolls to the form
  - empty form blocked by validation
  - lead form success state
  - partner form success state (including optional blank phone)
  - FAQ opens
  - mobile sticky bar visible
  - mobile menu opens
  - mobile headline visible
- The forms were tested with **network interception**, so no test leads were sent to the real inbox.

---

## Known follow-ups

- Have Ashley and Tracy click the FormSubmit activation links, then submit one test lead.
- For true source-level privacy, move the form behind a server-side relay or replace the endpoints with FormSubmit privacy aliases from the activation emails.
- Add the clinic's public phone when available (the clinic site lists 816-343-4883).
- Confirm consult/lab pricing.
- Have counsel review the alcohol offer before paid promotion.
- Add the Meta Pixel and UTM-tagged ad URLs.
- Remove `noindex` at official launch.
