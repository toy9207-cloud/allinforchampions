# allinforchampions.org

One-page site for All In For Champions and the NFR Celebrity Blackjack Tournament. Plain HTML and CSS, no build step.

- `index.html` — all page content
- `styles.css` — brand colors and layout
- `assets/` — logos, favicon, social share image
- `robots.txt`, `sitemap.xml`, `site.webmanifest`, `404.html` — search engine and browser files
- `CNAME` — tells GitHub Pages to serve the site at allinforchampions.org

## Go live on GitHub Pages (free)

1. Merge this branch into `main`.
2. Repo **Settings → Pages**: Source = "Deploy from a branch," branch = `main`, folder = `/ (root)`.
3. At the domain registrar, add these DNS records:
   - `A` records for `@` pointing to `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - `CNAME` record for `www` pointing to `toy9207-cloud.github.io`
4. Back in **Settings → Pages**, enter `allinforchampions.org` as the custom domain, wait for the DNS check, then tick **Enforce HTTPS**.

## After launch: Google Search Console

1. Go to search.google.com/search-console and add a **Domain** property for `allinforchampions.org`.
2. Choose the GoDaddy sign-in option so Google adds the verification record for you.
3. Under **Sitemaps**, submit `sitemap.xml`.
4. Under **URL Inspection**, enter `https://allinforchampions.org/` and click **Request indexing**.

## Email: info@allinforchampions.org

Pick one:

- **Google Workspace for Nonprofits (free with a verified 501(c)(3))** — full inbox, can send and receive as info@. Apply at google.com/nonprofits; verification runs through Goodstack and needs the EIN.
- **Google Workspace Business Starter (paid)** — same inbox, no verification wait.
- **Forwarding only (free, fastest)** — Cloudflare Email Routing or the registrar's forwarding sends info@ mail to an existing Gmail. Receiving works right away; sending *as* info@ takes extra setup.

Whichever option you choose, it adds `MX` and `TXT` records at the registrar. They don't conflict with the GitHub Pages records above.

## Open items

- Donation link: the Donate button and "Help us double our impact" section were removed until the page is ready; restore them from git history (commit da2e62e)
- Confirm the 501(c)(3) status shows up in the IRS Tax Exempt Organization Search for EIN 42-4855761
- Confirm the public player list, and get each player's OK before it goes up
- Brand fonts (Borensa, Sloop Script One) need a web license; Google Fonts stand-ins are used for now
