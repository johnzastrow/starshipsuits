# starshipsuits

Branding and public website for **Starship Suits**, a fursuit-making studio.

Production: [starshipsuits.com](https://starshipsuits.com) — domain at Porkbun,
hosted on Netlify. Neither is connected yet; see **Deployment** below.

## Status

A single coming-soon page, live-ready. Built in **Direction A, "Mission Patch"**
from `docs/02-visual-directions.html` — chosen because it is the one direction
that works before the studio has professional photography.

Direction A is not locked in. Everything visual is a CSS custom property in
`:root` plus one `@font-face` block, so moving to Direction B or C is a token
swap rather than a rewrite.

Not yet done: the real contact route (deliberately left out rather than
invented — see the comment in `web/index.html`), and the remaining six pages
specified in `docs/03-site-architecture.html`.

## Planning documents

Open `docs/index.html` in a browser. The set covers the brand brief, three
visual directions rendered with real type and colour, the site architecture, the
build and launch plan, and a technical profile of two competitor sites.

These are internal working documents and are **never published**. Both the
Netlify config (`publish = "web"`) and the Pages workflow stage `web/` only.

## Layout

```
web/                  the site - everything Netlify publishes
  index.html          landing page
  assets/css/         stylesheets
netlify.toml          publish dir, security headers, cache policy
docs/                 internal planning documents - not published
.github/workflows/    GitHub Pages staging deploy
.github/dependabot.yml
```

## Stack

Plain HTML and CSS. No framework, no build step, no backend, no server-side
state. The site is self-contained and loads no third-party scripts, fonts, or
stylesheets.

Adopting a Netlify template would change this — the templates in Netlify's
gallery are all framework-based (Astro, Next.js, Hugo) and introduce a build
step and a dependency tree. If one is adopted, update `netlify.toml`'s `command`
and `publish` accordingly, and add the matching ecosystem to
`.github/dependabot.yml`.

## Local preview

Any static file server works:

```sh
cd web && python3 -m http.server 8000
```

Then open <http://localhost:8000>.

## Deployment

**Production — Netlify.** `netlify.toml` is committed and complete. To go live:

1. In Netlify, *Add new site → Import an existing project → GitHub*, and pick
   `johnzastrow/starshipsuits`. Netlify reads `netlify.toml`; no build settings
   need to be entered by hand. (Netlify's free tier deploys from private
   repositories, so this repo does not have to be public.)
2. Add the custom domain `starshipsuits.com` in *Domain management*.
3. At Porkbun, point DNS at Netlify — see `docs/04-build-plan.html`.
4. Let Netlify provision the Let's Encrypt certificate, then enable
   *Force HTTPS*.

Every push to `main` then deploys; pull requests get deploy previews.

**Staging — GitHub Pages.** Currently **disabled**. Pages is unavailable for
private repositories on a free plan, so the workflow fails at `configure-pages`.
Once this repository is public: set *Settings → Pages → Source* to
"GitHub Actions", then `gh workflow enable "Deploy staging to Pages"`.

## Security notes

The site is static and public, so server-side concerns (auth, sessions, database
access, secrets) do not apply. What does:

- **Real headers come from Netlify.** `netlify.toml` sets CSP (including
  `frame-ancestors 'none'`), HSTS, `X-Content-Type-Options`, `Referrer-Policy`,
  `Permissions-Policy`, and `Cross-Origin-Opener-Policy`. GitHub Pages cannot set
  headers at all, so staging falls back to a `<meta>` CSP — which cannot express
  `frame-ancestors`, leaving staging framable. Production is the authority.
- **No third-party origins.** The CSP is `default-src 'self'`. Adding analytics,
  an embedded video, a map, or a hosted font requires widening it deliberately,
  one origin at a time — never to a wildcard. Fonts must be self-hosted.
- **A template changes this calculus.** Framework templates pull in a dependency
  tree and often load third-party assets. Review what any adopted template
  fetches at runtime before pointing DNS at it, and widen the CSP explicitly
  rather than removing it.
- **No secrets belong in this repo.** There is no server side to hold one.

## License

Source code is MIT licensed; see `LICENSE`. Brand assets — names, logos,
wordmarks, and other identity material — are not covered by that grant.
