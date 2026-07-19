# Dr. Metin — Online Consultation Website

A bilingual (Turkish / English) Jekyll website for a Turkey-based doctor, designed
around a **safe payment model**: the site never touches card data — patients pay on
**Shopier's** secure hosted page, book through a free scheduler (Cal.com), and meet
over Google Meet.

> ⚠️ **Read `COMPLIANCE` below before going live.** In Turkey, formal remote clinical
> care is regulated (2022 *Uzaktan Sağlık Hizmetleri* Yönetmeliği). This site is built
> as an **information + booking + second-opinion** site by default. Have a Turkish
> health-law / KVKK lawyer review the framing and the `legal/` pages.

---

## 1. What's in here

```
_config.yml            ← main settings (name, links, integrations)
_data/t.yml            ← ALL page text, TR + EN (edit copy here)
_data/services.yml     ← your service menu + prices
_layouts/, _includes/  ← templates (rarely need editing)
assets/css/main.scss   ← styling (colours near the top)
index.html             ← home
about / services / booking / contact .html
legal/*.html           ← disclaimer, KVKK, privacy, terms, refund (DRAFT templates)
.github/workflows/      ← auto-build & deploy to GitHub Pages
```

**Where to edit things**
- Your name, title, e-mail, and all integration links → `_config.yml`
- Any visible wording → `_data/t.yml` (keep the `tr:` and `en:` sides in sync)
- Prices and the list of services → `_data/services.yml`
- Colours → the `:root { ... }` block at the top of `assets/css/main.scss`

---

## 2. Run it on your computer (Windows)

1. Install **Ruby+Devkit** from https://rubyinstaller.org (pick the latest x64 "with DevKit").
   At the end, let it run `ridk install` (choose option 3).
2. Open a new terminal in this folder and run:
   ```powershell
   gem install bundler
   bundle install
   bundle exec jekyll serve --livereload
   ```
3. Open http://127.0.0.1:4000 → Turkish site. English is at http://127.0.0.1:4000/en/

**Before you push, test the language switch:** click `EN` / `TR` on a few pages and
confirm each page has a working counterpart. (Mismatched pages are the usual bug.)

---

## 3. Publish free on GitHub Pages

1. Create a GitHub repository and push this folder to it (branch `main`).
2. In the repo: **Settings → Pages → Build and deployment → Source = "GitHub Actions"**.
   (This is required — the default Pages build cannot run the bilingual plugin.)
3. Every push to `main` now builds and publishes automatically (see the **Actions** tab).

### Custom domain + HTTPS (recommended)
1. Buy a domain, then **Settings → Pages → Custom domain** → enter it.
2. At your DNS provider add either:
   - an apex domain: four `A` records → `185.199.108.153`, `.109.153`, `.110.153`, `.111.153`
   - or a `www` subdomain: a `CNAME` → `<your-username>.github.io`
3. Wait for the certificate (up to ~24h), then tick **Enforce HTTPS**.
4. Set `url:` in `_config.yml` to your domain and keep `baseurl: ""`.

> Using a project subpath (`username.github.io/repo`) instead of a domain? Set
> `baseurl: "/repo"` in `_config.yml`. A custom domain is simpler and looks more
> professional for a clinic.

---

## 4. Turn on the interactive pieces

All four are optional and independent — fill the matching field in `_config.yml`.

| Feature | Tool | What to do | Field in `_config.yml` |
|---|---|---|---|
| **Payments (planned)** | **Shopier** | Create a Shopier product for the 1000 TL planned services and paste its link. | `payments.planned_shopier_url` |
| **Booking** (planned) | **Cal.com** (free) | Create an account + a 30-min event, copy your public booking URL. | `booking.cal_url` |
| **Video** (planned) | **Google Meet** | In Cal.com, connect your Google Calendar and set the event location to **Google Meet** — a Meet link is added to every booking automatically. Nothing to paste here. | (auto via Cal.com) |
| **Quick consult** | **Shopier** (pay-to-reveal) | Create a Shopier product for the Quick Consultation. In its **"Sipariş Onay Mesajı"** (post-payment confirmation message) put your WhatsApp link (`https://wa.me/9050...?text=...`). Paste the product link here. The number is shown ONLY after payment — never put it in this repo (the repo is public). | `payments.quick_shopier_url` |
| **Contact form** | **Web3Forms** (free) | Get a free access key at web3forms.com. | `forms.web3forms_key` |

**Two patient flows this creates:**
- **Planned** (video / second opinion / test review): `pick a time (Cal.com)` → `pay on Shopier` → `you confirm the booking & the Google Meet link is emailed automatically`. Set the Cal.com event to "requires confirmation" so you approve after seeing the payment.
- **Quick consultation** (pay-to-reveal): `tap "Pay & connect"` → `pay on Shopier` → `Shopier's confirmation message reveals your WhatsApp link` → `patient messages you`.

> Both use **Shopier** because it onboards Turkey-based merchants, allows consultation services, and (for the quick one) its order-confirmation message can hold your WhatsApp link, shown only after payment.

Because payment always happens on Shopier's PCI-DSS page, **card data never reaches this site.**

> Why not Stripe/PayPal? Both are unavailable to Turkey-registered accounts. Shopier /
> iyzico / PayTR are the Turkey-correct choices; a globally-branded checkout (Stripe)
> would require forming a foreign company — only worth it at higher volume.

---

## 5. COMPLIANCE — before you go live

- [ ] Have a **health-law / KVKK lawyer** review the framing and rewrite the `legal/*.html`
      templates (they are marked DRAFT for a reason).
- [ ] Confirm with your lawyer / **tabip odası** whether your *muayenehane* needs a
      Ministry-of-Health **remote-health permit** for any formal clinical service.
- [ ] Keep the site to **information / second opinion / booking**; do not advertise
      guaranteed outcomes or "prescriptions on demand".
- [ ] **Never** collect symptoms / diagnoses / medical history through the contact form
      (health data is special-category under KVKK & GDPR). The form warns users already.
- [ ] Be cautious with patients **physically located abroad** — check licensing in their
      country and your **indemnity insurance** territorial cover.
- [ ] Fill in the bracketed `[ ]` placeholders in the legal pages (dates, refund window).
- [ ] Add a "not for emergencies — call 112" line everywhere consultations are offered
      (already in the footer and disclaimer).

*This README and the legal templates are general information, not legal advice.*
