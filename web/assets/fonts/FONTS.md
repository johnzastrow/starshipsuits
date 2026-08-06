# Fonts

Both families are self-hosted rather than loaded from a CDN. The site's
Content-Security-Policy is `default-src 'self'`, so a third-party font request
would be blocked outright — and beyond the policy, a CDN font puts another
company on the render path and discloses every visitor's IP address to them.

These are Latin-subset builds only. If the site ever needs extended Latin,
Cyrillic, Greek, or Vietnamese coverage, add those subsets as separate
`@font-face` rules with matching `unicode-range` descriptors rather than
swapping these for the full families.

| File | Family | Weights | Size |
|---|---|---|---|
| `archivo-latin-var.woff2` | Archivo (variable: `wght` 400–900, `wdth` 62–125%) | all | 88 KB |
| `martianmono-latin-400.woff2` | Martian Mono | 400 | 10 KB |
| `martianmono-latin-700.woff2` | Martian Mono | 700 | 10 KB |

## Licensing

Both are licensed under the **SIL Open Font License, Version 1.1**, which
permits embedding and redistribution provided the license accompanies the font
files. The full text is in `OFL.txt` alongside this file.

- **Archivo** — Copyright © The Archivo Project Authors (Omnibus-Type).
  <https://github.com/Omnibus-Type/Archivo>
- **Martian Mono** — Copyright © Evil Martians.
  <https://github.com/evilmartians/mars-mono>

Neither font may be sold on its own, and any derivative must not use the
reserved font names. Ordinary use on this website is fully permitted.

Note that this is separate from the repository's own MIT `LICENSE`: the MIT
grant covers the site's source, not these third-party font binaries.
