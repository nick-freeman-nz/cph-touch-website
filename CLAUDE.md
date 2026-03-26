# CPH Touch Website — Project Notes

## Stack
Single `index.html` file with embedded CSS and JS. All assets (logos, photos) are local files in the repo. No build process, no dependencies.

## Hosting Plan
- **GitHub** — source of truth for all code and images
- **Netlify** — auto-deploys on every push to main branch
- **Domain** — `copenhagentouchrugby.dk` purchased from [simply.com](https://simply.com), pointed to Netlify

### Deploy workflow
```
Edit index.html → commit & push to GitHub → Netlify auto-deploys → live in ~1 min
```

## Domain & DNS Status

### copenhagentouchrugby.dk → CPH Touch Website
- **Registrar:** Simply.com
- **DNS records configured:**
  - `A @ → 75.2.60.5`
  - `A @ → 99.83.190.102`
  - `CNAME www → cph-touch-website.netlify.app`
- **Primary domain in Netlify:** `copenhagentouchrugby.dk` (without www)
- **SSL status:** ⏳ Pending — DNS was added 2026-03-26, waiting for global propagation. Once [dnschecker.org](https://dnschecker.org/) shows the A record globally, hit "Renew certificate" in Netlify → HTTPS section.
- **Next step:** Check SSL cert provisioning. If still failing, wait up to 24h for full `.dk` propagation then retry.

## Workflow Rules
- **Always push to GitHub** after making changes. Every change should be committed and pushed — don't wait for the user to ask.

## Before Going Live — Checklist

### 🔴 Must fix
- [ ] **Contact form** — wire up to [Formspree](https://formspree.io) (free). Currently fakes submission, nothing is sent. Users think they've messaged but you never receive it.
- [ ] **Form validation** — add `required` attributes to name/email fields
- [ ] **Privacy Policy** — GDPR requirement (Denmark/EU). Collecting names & emails via contact form legally requires a policy explaining data use.
- [ ] **Payment details** — replace placeholder `#XXXXXX` MobilePay number and `XXXX/XXXXXXXXXX` bank details with real values

### 🟡 Do soon
- [ ] **Social media links** — replace all `href="#"` on Instagram, Facebook, X with real URLs
- [ ] **Real email** — confirm `info@cphtouch.dk` is live and monitored
- [ ] **Flag images** — emoji flags don't render on Windows. Swap to `flag-icons` CSS library (CDN, free)

### 🟢 Nice to have
- [ ] **Compress photos** — current total ~11MB. Use [squoosh.app](https://squoosh.app) to get to ~2-3MB. Faster load on mobile.
- [ ] **Meta description** — add `<meta name="description">` for Google search results
- [ ] **Pause particle canvas off-screen** — saves battery on mobile (IntersectionObserver on hero)
- [ ] **Self-host Google Fonts** — removes Google IP tracking (minor GDPR concern, low priority)

## Images
All photos are from Touchtober 2025, stored in `/Touchtober 2025/`. Paths in HTML are relative — they just work as long as folder structure is maintained in the repo.

**GitHub image limits:** 100MB per file, keep repo under 1GB total. At ~250KB per compressed photo you have headroom for thousands of photos. Organise future seasons in subfolders:
```
images/
  touchtober-2025/
  touchtober-2026/
  training/
```

## Known Placeholders
| Location | Placeholder | What's needed |
|---|---|---|
| Membership section | `#XXXXXX` | Real MobilePay number |
| Membership section | `XXXX / XXXXXXXXXX` | Real bank reg + account number |
| Contact section | `info@cphtouch.dk` | Confirm this email exists |
| Social links | `href="#"` | Real Instagram / Facebook / X URLs |
| Events | Spring 2026 / Oct 2026 | Real dates when known |
| Training times | 10:00–12:00 / 18:00–20:00 | Confirm or update |
| Training location | Fælledparken | Confirm or update |

## Security Notes
- No API keys or secrets in the codebase — safe to keep repo public
- HTTPS handled automatically by Netlify (Let's Encrypt) once DNS propagates
- Contact form currently has no backend — **fix before launch** (Formspree)
- Google Fonts loads from external CDN (minor GDPR note — self-host if strict compliance needed)
