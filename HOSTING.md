# Putting the site online

The site is one folder of static files. No server, no database, no monthly bill.
Pick one of these.

---

## Option A — Netlify Drop (free, ~60 seconds, no account needed to start)

The fastest way to get a working link today.

1. Unzip `pratiksha-3d-website.zip`.
2. Go to **https://app.netlify.com/drop**
3. Drag the **`site`** folder onto the page.
4. You get a live URL immediately, something like
   `https://cheerful-marzipan-4f21a8.netlify.app`.
5. Sign up (free) when prompted so the site is saved to an account, otherwise it
   expires.
6. To rename it: Site configuration → Change site name → `pratiksha-enterprises`
   gives you `https://pratiksha-enterprises.netlify.app`.

Free tier is far more than this site will ever need. HTTPS is automatic.

---

## Option B — GitHub Pages (free, permanent, you already have an account)

Your account is `kshatipra`. I could not create the repository from here (this
session only has access to repositories it has been explicitly connected to), so
these are the steps for you.

1. Go to **https://github.com/new**
   - Repository name: `pratiksha-enterprises`
   - Public
   - Tick **Add a README file**
   - Create repository
2. On the repo page: **Add file → Upload files**
3. Drag in the **contents** of the `site` folder — `index.html`, `robots.txt`,
   `sitemap.xml`, `.nojekyll`. Not the folder itself, the files inside it.
4. Commit changes.
5. **Settings → Pages**
   - Source: *Deploy from a branch*
   - Branch: `main`, folder: `/ (root)`
   - Save
6. Wait about a minute. The site appears at
   **https://kshatipra.github.io/pratiksha-enterprises/**

To update later, upload a new `index.html` over the old one.

---

## Option C — Your own domain (₹500–900 a year)

Worth doing once the shop starts putting the address on bills and the signboard.

1. Buy **pratikshaenterprises.in** from GoDaddy, BigRock, Hostinger or
   Cloudflare Registrar (Cloudflare is cheapest and does not do renewal
   price hikes).
2. Host with Option A or B above, then add the domain:
   - **Netlify:** Domain management → Add a domain → follow the DNS instructions.
   - **GitHub Pages:** Settings → Pages → Custom domain.
3. Both give free HTTPS automatically. Give DNS a few hours to take effect.
4. Then edit two lines near the top of `index.html` so search engines record the
   right address — search for `pratikshaenterprises.in` and update the
   `canonical` and `og:url` values, plus the one in `sitemap.xml`.

### If you already pay for Indian hosting (Hostinger / BigRock / GoDaddy)

Use the **`site-multifile`** folder instead. Open File Manager or connect by FTP
and upload its contents into `public_html/`. `index.html` must sit directly in
`public_html`, not inside a sub-folder.

---

## After it is live

1. **Google Business Profile** — business.google.com. Search for the shop first
   and *claim* any existing listing rather than making a second one. Primary
   category: Print shop. Take the video verification option if offered; it is
   much faster than the postcard. Add the website URL once you have it.
2. **Google Search Console** — search.google.com/search-console → add your
   domain → Sitemaps → submit `sitemap.xml`. This tells Google the page exists
   instead of waiting to be found.
3. **Justdial** — there is a "Claim this business" link on the existing listing.
   Add the website URL and the phone number there too.
4. Keep the phone number **identical** on the website, Google and Justdial.
   Google cross-checks them and mismatches push you down in local results.
