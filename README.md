# starshipsuits

Branding and public website for starshipsuits.

## Status

Scaffold. The visual direction has not been chosen yet, and `index.html` is a
neutral placeholder standing in for the real landing page.

## Stack

Plain HTML, CSS, and JavaScript. No framework, no build step, no backend, and no
server-side state. The site is entirely static and self-contained: it loads no
third-party scripts, fonts, or stylesheets.

## Layout

```
index.html            landing page
assets/css/           stylesheets
.github/workflows/    GitHub Pages staging deploy
.github/dependabot.yml
```

## Local preview

Any static file server works. With Python installed:

```sh
python3 -m http.server 8000
```

Then open <http://localhost:8000>.

## Deployment

- **Staging** — GitHub Pages, published from `main` by
  `.github/workflows/pages.yml` on every push.
- **Production** — hosted outside GitHub. The host has not been chosen yet, so
  no production deploy configuration is committed. See the security note below
  about response headers, which must be configured on whichever host is picked.

## Security notes

The site is static and public, so the usual server-side concerns (auth,
sessions, database access, secrets) do not apply. What does apply:

- **Response headers are a production-host responsibility.** GitHub Pages cannot
  set custom HTTP headers, so staging relies on a `Content-Security-Policy`
  `<meta>` tag. A `<meta>` CSP cannot express `frame-ancestors`, so clickjacking
  protection is unavailable on staging. The production host must set real
  headers: `Content-Security-Policy` (including `frame-ancestors 'none'`),
  `Strict-Transport-Security`, `X-Content-Type-Options: nosniff`, and
  `Referrer-Policy`.
- **No third-party origins.** The CSP is `default-src 'self'` and everything the
  page needs is served from this repo. Adding an external font, analytics
  snippet, or CDN script means widening that policy, and any such script needs
  Subresource Integrity.
- **No secrets belong in this repo.** It is public and has no server side that
  could hold a credential.

## License

Source code is MIT licensed; see `LICENSE`. Brand assets — names, logos,
wordmarks, and other identity material — are not covered by that grant.
