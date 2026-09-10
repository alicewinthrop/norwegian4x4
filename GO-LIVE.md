# Go-live checklist: norwegian4x4.app

Steps to take the site live on the custom domain and get it indexed. Do them
in order. Items marked "one time" only need doing once.

## 1. Point DNS at GitHub Pages (Namecheap, one time)

In Namecheap, open the domain and go to **Advanced DNS**. Under **Host Records**,
add these records. Delete any default parking or "CNAME @ parkingpage" record
Namecheap added, or it will conflict.

| Type | Host | Value | TTL |
| :--- | :--- | :--- | :--- |
| A | @ | 185.199.108.153 | Automatic |
| A | @ | 185.199.109.153 | Automatic |
| A | @ | 185.199.110.153 | Automatic |
| A | @ | 185.199.111.153 | Automatic |
| CNAME | www | alicewinthrop.github.io. | Automatic |

Optional but recommended, add IPv6 as well:

| Type | Host | Value |
| :--- | :--- | :--- |
| AAAA | @ | 2606:50c0:8000::153 |
| AAAA | @ | 2606:50c0:8001::153 |
| AAAA | @ | 2606:50c0:8002::153 |
| AAAA | @ | 2606:50c0:8003::153 |

DNS can take from a few minutes to a couple of hours to propagate.

## 2. Merge this branch into main

GitHub Pages builds the site from the `main` branch. Merge `claude/landing-page`
into `main`. The `CNAME` file in this repo already contains `norwegian4x4.app`.

## 3. Set the custom domain in GitHub Pages (one time)

Repo **Settings > Pages**:

1. Under **Custom domain**, enter `norwegian4x4.app` and click **Save**.
2. Wait for the DNS check to pass (it can take a while after step 1).
3. Tick **Enforce HTTPS**. The `.app` domain is on the HSTS preload list, so
   HTTPS is required. GitHub provisions a certificate automatically; the site
   will not load over HTTP, and the certificate can take up to an hour.

Once this passes, `https://alicewinthrop.github.io/norwegian4x4/` and the `www`
subdomain both redirect to `https://norwegian4x4.app/`.

## 4. Verify the site

- `https://norwegian4x4.app/` loads the landing page over HTTPS.
- `https://norwegian4x4.app/what-is-the-norwegian-4x4-workout/` loads the guide.
- `https://norwegian4x4.app/support` and `/privacy-policy` load.
- `https://norwegian4x4.app/sitemap.xml` and `/robots.txt` load.

## 5. Google Search Console (one time)

1. Go to Google Search Console and add a **Domain** property for `norwegian4x4.app`.
2. Verify it by adding the TXT record it gives you in Namecheap Advanced DNS.
3. Submit `https://norwegian4x4.app/sitemap.xml` under **Sitemaps**.
4. Use **URL Inspection** to request indexing for the home page and the guide.

## Content to fill in (not blocking go-live)

- **Real App Store link.** Replace the placeholder `idXXXXXXXXX` in the App Store
  links. It appears in `index.html` (2 places) and
  `what-is-the-norwegian-4x4-workout/index.html` (1 place).
- **Social share image.** Add a 1200x630 image at `/assets/og-image.png`. It is
  referenced by the Open Graph and Twitter tags on both pages.
- **Screenshots and visual design.** The pages have marked placeholder slots for
  screenshots (from the app repo `assets/screenshots/`) and are otherwise
  minimally styled, ready for the design system.

## After the domain resolves

- In App Store Connect, update the Support URL to `https://norwegian4x4.app/support`
  and the Privacy Policy URL to `https://norwegian4x4.app/privacy-policy`. Do this
  only after step 4 passes. The old github.io URLs keep working via redirect, so
  there is no rush.

## Off-page, to actually rank

- Launch on Product Hunt.
- Post where the 4x4 comes up naturally: r/running, r/AdvancedRunning, r/tabata,
  and running forums. Link only when it genuinely helps the thread.
- Link to the site from the App Store listing, and from the app itself.
- List in a few fitness-app directories.
