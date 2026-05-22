# mjr-blog-site

## What this project does
Portfolio and blog website for Mark Reynolds at markjreynolds.com. Built with Hugo Extended (static site generator) and the Congo v2 theme. Deployed via Vercel with automatic CI/CD on every push to GitHub. Currently staging at build.markjreynolds.com; production domain markjreynolds.com to be configured when ready.

## Stack
- **Generator:** Hugo Extended v0.161.1
- **Theme:** Congo v2.13.0 (git submodule at `themes/congo`, stable branch)
- **Config:** Split-config pattern at `config/_default/`
- **Hosting:** Vercel — build command `hugo --gc --minify`, output dir `public/`
- **Repo:** https://github.com/Samesphere/mjr-blog-site

## Current status
- Hugo site initialised with Congo theme
- Card grid homepage, search enabled, reading time, TOC on articles
- Initial content: homepage, about page, hello-world post
- Staged at build.markjreynolds.com (connect in Vercel dashboard — see deployment steps below)
- Production domain markjreynolds.com: not yet configured

## Deployment steps (one-time Vercel setup)
1. Go to vercel.com → New Project → Import from GitHub → select `mjr-blog-site`
2. Hugo is auto-detected; `vercel.json` supplies build command and output dir
3. Add environment variable: `HUGO_VERSION = 0.161.1`
4. Deploy → note the `.vercel.app` URL
5. In Project Settings → Domains, add `build.markjreynolds.com`
6. At registrar: add CNAME `build` → `cname.vercel-dns.com`

## Going live on markjreynolds.com
1. Update `baseURL` in `config/_default/hugo.toml` to `https://markjreynolds.com/`
2. In Vercel: add `markjreynolds.com` as a domain
3. At registrar: point apex domain to Vercel (A records or ALIAS)

## Content
- Posts: `content/posts/<slug>/index.md` (use page bundles so images live alongside the post)
- About: `content/about/index.md`
- Homepage intro: `content/_index.md`
- Tags and categories set in post front matter

## Local development
```powershell
hugo server -D   # live reload at http://localhost:1313, includes drafts
hugo --gc --minify   # production build check
```

## Customisation notes
- `layouts/_partials/functions/warnings.html` overrides the Congo theme partial to fix a Hugo 0.161.1 compatibility issue (`.Author` field removed from page context)
- Author social links: edit `config/_default/languages.en.toml` → `[params.author]`
- Color scheme: edit `config/_default/params.toml` → `colorScheme` (options: congo, slate, ocean, fire, forest, princess, neon)
