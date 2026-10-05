# ATOZ Tubing Services

Source for the ATOZ Tubing Services Ltd. website: **https://www.atoztubingservices.com/**

It's a single-page static site (plain HTML, CSS and JavaScript) built on the [Start Bootstrap "Grayscale"](https://startbootstrap.com/theme/grayscale) theme (Bootstrap 3 + jQuery). There's no build step, no server code and no database.

---

## How it's hosted

The site is served for free by **GitHub Pages** directly from this repository.

| Item | Value |
|---|---|
| Hosting | GitHub Pages |
| Branch that is published | **`gh-pages`** |
| Custom domain | `www.atoztubingservices.com` (set by the `CNAME` file on `gh-pages`) |
| Build process | None — files are served exactly as committed |

> **Important:** only the `gh-pages` branch is live. The `master` branch is an old copy of the starting template (its `CNAME` still points to `atoz.enek.net`) and is **not** what visitors see. Make all website changes on `gh-pages`.

### Custom domain / DNS

The `CNAME` file in the root of `gh-pages` tells GitHub Pages which domain to answer for. Don't delete or rename it, or the custom domain will stop working.

The domain's DNS (managed at the domain registrar / DNS provider for `atoztubingservices.com`) must point at GitHub Pages:

- `www` → `CNAME` record to `enek.github.io`
- Apex `atoztubingservices.com` (optional, redirects to `www`) → `A` records to GitHub's Pages IPs: `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`

GitHub's current values are documented here: [Managing a custom domain for your GitHub Pages site](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site).

The Pages settings (published branch, custom domain, "Enforce HTTPS") live in the repo under **Settings → Pages**. See [Configuring a publishing source for your GitHub Pages site](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site).

---

## How to modify the website

Any commit pushed to `gh-pages` is published automatically, usually within a minute or two. You can check progress under the repo's **Actions** tab (the "pages build and deployment" run).

### Option 1 — Edit in the browser (small text changes)

1. Go to https://github.com/enek/ATOZTubing and switch the branch selector to **`gh-pages`**.
2. Open the file (usually `index.html`) and click the pencil (Edit) icon.
3. Make the change, then click **Commit changes** and commit directly to `gh-pages`.
4. Wait a minute or two, then reload https://www.atoztubingservices.com/ (hard refresh with Ctrl+Shift+R / Cmd+Shift+R if you still see the old version).

To replace an image or brochure, open the `img/` or `files/` folder on `gh-pages` and use **Add file → Upload files**. Uploading a file with the **same name** replaces it without needing any HTML changes.

### Option 2 — Edit locally (larger changes)

```bash
git clone https://github.com/enek/ATOZTubing.git
cd ATOZTubing
git checkout gh-pages

# preview locally at http://localhost:8000
python3 -m http.server 8000

# after editing
git add .
git commit -m "Describe the change"
git push origin gh-pages
```

Preview locally before pushing — whatever is pushed to `gh-pages` goes live.

---

## Where things are

| What you want to change | Where |
|---|---|
| Page title, navigation, all text sections (About, Services, Safety, Contact) | `index.html` (each section is a `<section id="...">`) |
| Footer / copyright year | Bottom of `index.html` (`<footer>`) |
| Colours, fonts, spacing | `css/grayscale.css` (`index.html` loads this file) |
| Logos and photos | `img/` (`intro-bg.jpg` is the large header background; `img/ATOZLOGO.ai` is the logo's Illustrator source file) |
| Service brochures (PDFs linked from the Services section) | `files/brochure1.pdf` (Connection Supervision), `files/brochure2.pdf` (Computer Torque Monitoring) |
| Map centre, zoom and marker pin | `js/grayscale.js` (`google.maps.LatLng(...)` for the centre, `setZoom(...)`, and `myLatLng` for the marker pin) |
| Bootstrap, jQuery, Font Awesome | `vendor/` — third-party libraries, don't edit |

### Contact form

The contact form in `index.html` doesn't send email itself. It posts to **Jotform** (form ID `62876919236268`, `action="https://submit.jotform.ca/submit/62876919236268/"`). Where submissions go, email notifications, and spam settings are managed in the Jotform account that owns that form, not in this repo. If you add or rename form fields, the matching fields must also exist in the Jotform form.

### Google Map

The map is loaded with a Google Maps JavaScript API key in the `<script>` tag near the bottom of `index.html`. The key belongs to a Google Cloud project; if the map stops loading, check that project's billing and API settings. Because the key is visible in this public repo, it should be restricted to the `www.atoztubingservices.com` domain (HTTP referrer restriction) in the Google Cloud Console.

---

## Troubleshooting

- **Change isn't showing:** confirm you committed to `gh-pages` (not `master`), check the Actions tab for a failed build, then hard-refresh the browser.
- **Site shows a GitHub 404 or the domain stops working:** check that the `CNAME` file still exists on `gh-pages` and contains `www.atoztubingservices.com`, and that **Settings → Pages** still lists that custom domain.
- **HTTPS warning:** in **Settings → Pages**, make sure "Enforce HTTPS" is ticked. GitHub issues the certificate automatically once DNS is correct.
