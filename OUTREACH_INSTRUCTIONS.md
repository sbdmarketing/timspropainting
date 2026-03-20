# AI Agent Instructions: Populate Outreach Homepage Template

## Context
This is a pre-built Eleventy (11ty) static site used as a redesigned homepage lead magnet. Your job is to populate it with one real business's content. **Do not build anything from scratch — only replace content inside the existing files.**

---

## Defaults (use these when specific info is unavailable)
- **Social links**: Leave `facebook` and `instagram` as the generic placeholders in `client.js`. Do not look them up.
- **Business hours**: Default to `Mon–Fri: 9am – 5pm` / `Weekends: By Appointment`.
- **Address**: Use **city and state only** (e.g., `Chicago, IL`). No street address unless clearly listed.
- **Email**: Default to `info@[their domain]` unless a real email is found.

---

## Strict Rules — Read First

> [!CAUTION]
> **Do NOT touch image `src` or `srcset` attributes** — EXCEPT in the "Image Hotlinks" step below. Icons, logo, arrow SVGs, and all other images must remain completely untouched.

> [!IMPORTANT]
> **Do NOT change the number of elements** in any section. If the template has 4 service cards and the business only has 3 services, keep all 4 — invent a logical 4th that fits the industry.

> [!IMPORTANT]
> **Do NOT edit HTML structure, CSS classes, Nunjucks tags (`{% %}`/`{{ }}`), or JavaScript.** Only replace visible text and `href`/`alt`/`tel:`/`mailto:` values.

> [!CAUTION]
> **Do NOT add `layout:` to `index.html` front matter.** The template uses `{% extends "layouts/base.html" %}` as a Nunjucks block — adding a `layout:` key will break the build with "layout not found" errors. Also **do NOT remove** the `{% block head %}`, `{% block body %}`, or `{% endblock %}` tags that wrap the page content.

---

## Step 1 — Research the Business

Visit every URL provided. Extract:
- Business name, phone, email
- City and state
- Tagline or value proposition
- Full list of services
- Any trust signals: years in business, project count, guarantees, awards

---

## Step 2 — Edit `src/_data/client.js`

Replace every field:

```
name           → Business's brand name
email          → info@[domain] unless a specific email is found
phoneForTel    → Digits only, no formatting (e.g. "7087526996")
phoneFormatted → Display format (e.g. "(708) 752-6996")
address.lineOne → ""  (leave blank)
address.lineTwo → ""  (leave blank)
address.city   → City name only (e.g. "Chicago")
address.state  → Two-letter state abbreviation
address.zip    → ""  (leave blank)
address.mapLink → "https://www.google.com/maps/search/[Business+Name]+[City]+[State]"
socials.facebook  → leave as "https://www.facebook.com/"
socials.instagram → leave as "https://www.instagram.com/"
domain         → Business's website URL, no trailing slash
```

---

## Step 3 — Edit `src/index.html`

Edit only visible text and `href`/`alt` values. Work top to bottom:

### Front Matter
```
title       → "[Business Name] | [Primary Service] | [City, State]"
description → 140–160 char meta description
```

### Hero (`#hero-143`)
```
h1.cs-title     → Business name or tagline
p.cs-text       → 1–2 sentence value proposition
a.cs-button-solid → CTA text (e.g. "Get a Free Quote")
```

### Services Bar (`#h-services-143`) — **4 cards, keep all 4**
For each `.cs-item`:
```
h2.cs-title → Service name (1–4 words)
p.cs-text   → 1-sentence description
```
If fewer than 4 services exist, add a logical generic one for the industry.

### Gallery (`#gallery-43`)
```
span.cs-topper → e.g. "Our Work"
h2.cs-title    → e.g. "Projects That Speak for Themselves"
p.cs-text      → 1–2 sentences about their work quality
```

**6 gallery tiles** — each tile must have this structure, no exceptions:
```html
<a class="cs-item" href="/portfolio" data-lightbox="floorplans">
    <picture class="cs-picture">
        <img alt="[descriptive alt text]" ... />
    </picture>
    <div class="cs-hover-box">
        <picture class="cs-icon"><img ... /></picture>
        <h3 class="cs-h3">[Project/Service Name]</h3>
        <p class="cs-hover-box-text">[1 sentence description]</p>
    </div>
</a>
```
> [!CAUTION]
> Every tile MUST have its own closing `</picture>`, `cs-hover-box` div, and `</a>`. Missing any of these will cause tiles to not render or hover to break.

### Featured Service — SBS Reverse (`#sbsr-2289`)
Pick the business's flagship service.
```
span.cs-topper  → "Featured Service"
h2.cs-title     → Service name
p.cs-text       → 2–3 sentence description
h3.cs-h3        → "Key Features:"
li.cs-li ×3    → 3 key features or benefits
span.cs-number  → A stat number (e.g. "100+")
h3.cs-heading   → Stat label (e.g. "Projects Completed")
span.cs-desc    → Stat context (e.g. "across the Chicagoland area")
```

### Additional Services (`#gallery-2297`) — **3 cards, keep all 3**
```
span.cs-topper → "Additional Services"
h2.cs-title    → e.g. "More Ways We Can Help"
p.cs-text      → 1–2 sentences
```

> [!CAUTION]
> The `cs-gallery-wrapper` div must be **inside** `cs-container` — not a sibling of it. If the gallery images appear unstyled or full-width, check that the closing `</div>` for `cs-container` comes **after** `cs-gallery-wrapper`, not before it.

Each `.cs-image` card:
```
href           → "#"
span.cs-project → Service name
span.cs-tag    → "City, State"
```

### Stats Bar (inside `#gallery-2297`) — **4 stats, keep all 4**
```
span.cs-number → Number + unit (e.g. "200+", "5★", "100%")
span.cs-desc   → What it means (e.g. "Happy Clients")
```

### Side by Side (`#sbs-2295`) — **Before/After Section**
Pick the business's second most notable service.
```
span.cs-topper   → "Featured Service"
h2.cs-title      → Service name
p.cs-text        → 2–3 sentence description
h3.cs-h3         → "Our Process"
li.cs-li ×4     → 4 process steps (bold label + description each)
a.cs-button-solid → CTA (e.g. "Book a Consultation")
```

---

## Step 4 — Edit `src/_includes/components/footer.html`

### Contact Cards (top row) — 3 cards, keep all 3
```
Card 1 span.cs-card-info       → "City, State"
Card 2 span.cs-card-info[0]    → "Mon–Fri: 9am – 5pm"
Card 2 span.cs-card-info[1]    → "Weekends: By Appointment"
Card 3 a[href="tel:..."]       → href="tel:[phoneForTel]", text = formatted phone
Card 3 a[href="mailto:..."]    → href="mailto:[email]", text = email
```

### Logo & Description
```
img.cs-logo-img alt → "[Business Name] logo"
p.cs-text           → 1–2 sentence brand description
```

### Services Links — 3 links, keep all 3
Top 3 services as link text. All `href` → `"#"`.

### Useful Links — 4 links, keep all 4
About Us, Services, Contact Us + one more (Gallery, Reviews, etc.). All `href` → `"#"`.

### Contact Block
```
span.cs-topper[0]    → "Call Us"
a.cs-contact-link[0] → href="tel:[phoneForTel]", text = formatted phone
span.cs-topper[1]    → "Service Area" or "Location"
a.cs-contact-link[1] → href=[Google Maps URL], text = "City, State"
```

### Bottom Bar
```
a.cs-credit-link → Business name
```
Leave Terms and Privacy links as `"#"`.

---

## Step 5 — Apply Image Hotlinks

You will receive **13 image URLs** in numbered order. Apply them exactly as follows:

| # | Slot | Where |
|---|------|--------|
| 1 | **Hero** | In `index.html`: replace all 3 `src`/`srcset` values inside `#hero-143 .cs-background`. In `src/assets/sass/critical.scss` **line 182**: replace the `background: url(...)` value. |
| 2–7 | **6 Gallery tiles** | In `index.html`: replace the `src` on the `<img>` inside each `.cs-item .cs-picture` in `#gallery-43`, in order 1–6. |
| 8 | **SBS featured image** | In `index.html`: replace all `src`/`srcset` inside `#sbsr-2289 .cs-image-group .cs-picture`. |
| 9–11 | **3 Additional service cards** | In `index.html`: replace `src` on each `.cs-image .cs-picture img` in `#gallery-2297 .cs-gallery`, in order. |
| 12 | **Before image** | In `index.html`: replace all `srcset`/`src` in `#sbs-2295 .cs-picture1`. |
| 13 | **After image** | In `index.html`: replace all `srcset`/`src` in `#sbs-2295 .cs-picture2`. |

> [!CAUTION]
> Do NOT touch any other image `src` attributes — icons, logo, arrow SVGs, and graphic elements must stay exactly as they are.

---

## Quality Checklist

Before finishing, confirm:

- [ ] `client.js` has no `[placeholder]` values remaining
- [ ] `index.html` front matter `title` and `description` are filled in
- [ ] All 6 gallery tiles are present and each has its own `</picture>`, `cs-hover-box`, and `</a>`
- [ ] No `[bracket placeholders]` remain anywhere in `index.html` or `footer.html`
- [ ] Element counts are unchanged in every section (4 service cards, 6 gallery tiles, 3 additional cards, 4 stats, 4 process steps)
- [ ] `footer.html` phone uses `tel:` format and email uses `mailto:` format
- [ ] No CSS classes, Nunjucks tags (`{% %}`/`{{ }}`), or JavaScript was modified
- [ ] Only the 13 designated image slots were changed — no icons, logos, or SVGs

---

## Step 6 — Commit and Deploy

When the user gives the command **"commit and deploy"** or **"commit to github and deploy to vercel"**, run the `/deploy` workflow using the **Project Name** provided in the intake template.

The AI agent should automatically execute the `.agents/workflows/deploy.md` file to:
1. Initialize the Git repository
2. Push to a new GitHub repository
3. Link and deploy to Vercel

---

## ✂️ Intake Template — Copy and Paste This When Starting a New Client

```
BUSINESS URLS:
- Homepage:  
- Services:  
- About:     
- Contact:   

DEPLOYMENT:
- Project Name (for Vercel/GitHub): 

IMAGE HOTLINKS (provide 13 URLs in order):
1.  [Hero image]
2.  [Gallery tile 1]
3.  [Gallery tile 2]
4.  [Gallery tile 3]
5.  [Gallery tile 4]
6.  [Gallery tile 5]
7.  [Gallery tile 6]
8.  [SBS featured service image]
9.  [Additional service card 1]
10. [Additional service card 2]
11. [Additional service card 3]
12. [Before image]
13. [After image]
```

---