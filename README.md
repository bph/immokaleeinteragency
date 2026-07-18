# immokaleeinteragency

Website for the **Immokalee Interagency Council** — hosted as a static site on [GitHub Pages](https://pages.github.com/).

Live URL: <https://immokaleeinteragency.org>

---

## Repository layout

```
.
├── .github/
│   └── workflows/
│       └── deploy.yml   # GitHub Actions workflow – deploys to GitHub Pages
├── index.html           # Site homepage (replace with your migrated content)
├── CNAME                # Custom domain mapping for immokaleeinteragency.org
└── README.md
```

Add any additional HTML, CSS, JavaScript, images, or other static assets directly to the repository root (or subdirectories). Every push to the `main` branch triggers an automatic deployment.

---

## One-time setup (do this once in GitHub)

### 1. Enable GitHub Pages

1. Open the repository on GitHub and go to **Settings → Pages**.
2. Under **Build and deployment → Source**, select **GitHub Actions**.
3. Save. The first deployment will run automatically on the next push to `main`.

### 2. Configure the custom domain

The `CNAME` file in this repository already tells GitHub Pages to serve the site at `immokaleeinteragency.org`. You also need to add DNS records at your domain registrar:

| Type  | Host / Name           | Value                     |
|-------|-----------------------|---------------------------|
| A     | `@`                   | `185.199.108.153`         |
| A     | `@`                   | `185.199.109.153`         |
| A     | `@`                   | `185.199.110.153`         |
| A     | `@`                   | `185.199.111.153`         |
| CNAME | `www`                 | `bph.github.io`           |

> **Note:** `bph.github.io` is the correct value for this repository (GitHub user **bph**). If the repository is ever transferred to a different account, replace it with `<new-username>.github.io`.

DNS changes can take up to 48 hours to propagate. Once propagated, GitHub will automatically provision a free TLS certificate via Let's Encrypt.

After the DNS records are live, go back to **Settings → Pages**, verify that the custom domain shows no errors, and optionally tick **Enforce HTTPS**.

---

## Migrating existing site content

Follow these steps to copy the current content from immokaleeinteragency.org into this repository:

### Option A – Copy files manually

1. Download all pages, images, CSS, and JS from the existing host (ask your current host for an FTP/cPanel download, or use `wget` / `httrack` to crawl the site):
   ```bash
   wget --mirror --convert-links --adjust-extension \
        --page-requisites --no-parent \
        https://immokaleeinteragency.org/
   ```
2. Copy the downloaded files into the root of this repository (replace the placeholder `index.html`).
3. Commit and push to `main`. The Actions workflow will deploy automatically.

### Option B – WordPress / CMS export

If the existing site runs on WordPress or another CMS:

1. Use a plugin such as **Simply Static** or **WP2Static** to export a full static HTML snapshot.
2. Copy the exported files into this repository.
3. Commit and push to `main`.

---

## Making content updates after migration

1. Edit or add HTML/CSS/JS files in the repository.
2. Commit and push to `main`:
   ```bash
   git add .
   git commit -m "Update site content"
   git push
   ```
3. The GitHub Actions workflow (`.github/workflows/deploy.yml`) will automatically build and deploy the updated site within a minute or two.

---

## Local preview

Because the site is plain static HTML there is no build step. You can preview it locally with any static file server, for example:

```bash
# Python 3
python3 -m http.server 8000
# then open http://localhost:8000 in your browser
```

---

## Useful references

- [GitHub Pages documentation](https://docs.github.com/en/pages)
- [Managing a custom domain for GitHub Pages](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site)
- [Enforcing HTTPS on GitHub Pages](https://docs.github.com/en/pages/getting-started-with-github-pages/securing-your-github-pages-site-with-https)
