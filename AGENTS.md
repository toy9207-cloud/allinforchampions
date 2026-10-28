# AGENTS.md — allinforchampions.org

Handoff notes for any AI coding agent (Codex, Claude Code, etc.) working on this repo. Read this before changing anything.

## What this is

One-page website for **All In For Champions**, a nonprofit public charity (EIN 42-4855761) run by Courtney Motes and Megan McGill, who also own Seven X Custom Jewelry. The charity hosts the **NFR Celebrity Blackjack Tournament** during the Wrangler National Finals Rodeo in Las Vegas. 100% of funds raised go to **Golden Circle of Champions**, which supports children facing pediatric cancer and their families.

### Event facts (source: player invite letter)

- Friday, Dec. 4, 2026, 11 a.m., Virgin Hotels Las Vegas (4455 Paradise Road, Las Vegas, NV 89169)
- 10 NFR contestants + 5 VIP players; sponsors cover every buy-in
- Emcee: Lefty Holman. The Cowboy Channel films the event. Fans welcome to watch.
- 2025 raised $27,500; 2026 goal is to double it ($55,000)
- Players (as of Oct. 28, 2026): Cody Snow, Jordi Mitchell, Lane Mitchell, Rylee George, Haven Meged, Shelby Meged, Derrick Begay, Colter Todd, Cooper James. Spellings are confirmed by the owner. Do not "correct" them. Lefty Holman is the emcee, not a player; he has his own spot below the player grid and is `contributor` (not `performer`) in the JSON-LD.
- Presenting sponsors: Virgin Hotels Las Vegas (Curio Collection by Hilton), Seven X Custom Jewelry

## Stack and hosting

- Plain static HTML + CSS. **No build step, no framework, no JavaScript.** Keep it that way.
- Hosted on **GitHub Pages** from the `main` branch, root folder. Pushing to `main` deploys.
- Custom domain `allinforchampions.org` (registrar: GoDaddy). `CNAME` file must stay in the repo root.
- DNS at GoDaddy is done: four `A` records for `@` → 185.199.108.153 / .109.153 / .110.153 / .111.153, and `CNAME` `www` → `toy9207-cloud.github.io`. GitHub reports "DNS check successful."

## Files

| File | Purpose |
|---|---|
| `index.html` | All page content, SEO meta tags, JSON-LD structured data |
| `styles.css` | Brand palette (CSS variables in `:root`) and layout |
| `assets/` | `logo.webp` (main logo, transparent), sponsor logos (`.webp`), `og-image.jpg` (1200×630 share card), favicon and app icons |
| `robots.txt`, `sitemap.xml`, `site.webmanifest`, `404.html` | Search engine and browser files |
| `CNAME` | GitHub Pages custom domain |

## Brand rules

- Colors (from the brand guide): red `#D84444`, sand `#CBAF73`, light sand `#CEB181`, gold `#B08752`, black `#1F1A1E`, charcoal `#3D393C`, slate `#5B5155`. Off-white page background `#F7F3EC`.
- Brand fonts are Borensa (display) and Sloop Script One (script). They are licensed fonts, so the site uses Google Fonts stand-ins: Alfa Slab One, Pinyon Script, Jost (body). Swap only if the owner provides web-licensed font files.
- Copy is **AP style**, direct news tone, no fluff. Examples: "Dec. 4", "11 a.m.", no Oxford comma.
- Never use the 2025 white logo variant; it has the year baked in.
- "NFR" is a PRCA registered trademark. Keep the footer trademark line.

## Rules for changes

1. **Keep the player list in two places in sync**: the visible `<ul class="players">` in the `#players` section and the `performer` array in the JSON-LD `<script type="application/ld+json">` block in `index.html`.
2. Any event fact change (date, time, venue, sponsors) must be updated in the visible copy, the meta description / OG / Twitter tags, AND the JSON-LD `Event` block.
3. Validate the JSON-LD parses as JSON after editing.
4. When content changes, update `<lastmod>` in `sitemap.xml`.
5. Images: WebP, explicit `width`/`height`, `loading="lazy"` below the fold.
6. Check the page at 390px wide (phone) and 1280px wide before pushing.
7. Do not add analytics, cookie banners, trackers or third-party scripts without the owner asking.

## Open tasks

### 1. Donation link (waiting on the owner)
Donations were removed until the donation page exists (Zeffy is the recommended platform: no fees, so the "100% goes to Golden Circle" claim stays true). When the owner provides the URL:
- Restore the hero Donate button and the `<section class="cta" id="give">` block from commit `da2e62e` (`git show da2e62e:index.html`).
- Point both Donate buttons at the donation URL (open in the same tab).
- In the hero, Donate goes back to `btn-red` and "Become a Sponsor" goes back to `btn-outline`.
- If the platform offers an embeddable goal thermometer, add it to the `#give` section.

### 2. Player list and headshots
Headshots live in `assets/players/` as 400×400 WebP squares, named `first-last.webp`; CSS crops them to circles. Players without a photo show an initials circle (`<span class="avatar avatar-placeholder">`). To add a photo: crop square with the face centered and the hat fully in frame, save as WebP, then swap the `<span>` for `<img class="avatar" src="assets/players/first-last.webp" width="400" height="400" loading="lazy" alt="First Last">`. Current photos were collected Oct. 28, 2026, from PRCA, WPRA, Western Horseman, Rodeo on SI and American Hat Company pages at the owner's direction; the owner accepted the rights risk. Keep the photo credit line under the player grid. If a photographer or organization asks for removal, take the photo down and restore the initials circle. Replace with athlete-supplied photos when available.

Each player must OK being listed publicly. Remove anyone who hasn't, in both places (see rule 1). Add new players as they confirm.

### 3. Confirm 501(c)(3)
JSON-LD says `"nonprofitStatus": "Nonprofit501c3"`. Owner should confirm EIN 42-4855761 is listed at apps.irs.gov/app/eos. If not, change it to `"NonprofitType"` or remove the field.

## Manual setup that an agent CANNOT do

These need a human logged into GoDaddy, GitHub settings, or Google Admin. An agent can walk the owner through them but cannot click them.

### GitHub Pages HTTPS
Repo Settings → Pages → tick **Enforce HTTPS** once GitHub finishes issuing the certificate (up to 24 hours after the DNS check passes). If still unavailable after 24 hours: Remove the custom domain, re-enter `allinforchampions.org`, Save.

### Email: info@allinforchampions.org
**Decision:** add the domain to Seven X Custom Jewelry's existing Google Workspace as a secondary domain, with `info@` as a free Google Group. **Long term:** move to the charity's own Google Workspace for Nonprofits account (free with 501(c)(3) verification) after the December event, so the charity's email isn't owned by a for-profit business.

Steps (Seven X super admin, admin.google.com):
1. **Account → Domains → Manage domains → Add a domain** → `allinforchampions.org` → **Secondary domain** → verify using the **Sign in to GoDaddy** option. Then **Activate Gmail**, again via GoDaddy sign-in.
2. **Directory → Groups → Create group**: name "All In For Champions", email `info@allinforchampions.org`, owners Courtney and Megan. Set **Who can post** to **Anyone on the web / External**, or outside mail bounces.
3. Each owner, in Gmail: Settings → See all settings → Accounts → **Send mail as** → add `info@allinforchampions.org` → click the confirmation email.
4. GoDaddy DNS — add:
   - `TXT` `@` → `v=spf1 include:_spf.google.com ~all`
   - `TXT` `_dmarc` → `v=DMARC1; p=none; rua=mailto:info@allinforchampions.org`
   - DKIM: Admin console → Apps → Google Workspace → Gmail → **Authenticate email** → select the domain → Generate new record → add that `TXT` at GoDaddy → wait an hour → **Start authentication**.
5. GoDaddy DNS — **delete any old `MX` records pointing to `secureserver.net`**. Only Google's MX (`smtp.google.com`) should remain. Do not touch the GitHub `A`/`CNAME` records.
6. Test: send from a personal account to info@, confirm it arrives; reply as info@, confirm the From address.

After email works, update the brand guide contact from Seven X's address to info@allinforchampions.org.

### Google Search Console
search.google.com/search-console → add **Domain** property `allinforchampions.org` → verify via GoDaddy sign-in → Sitemaps: submit `sitemap.xml` → URL Inspection: `https://allinforchampions.org/` → Request indexing.
