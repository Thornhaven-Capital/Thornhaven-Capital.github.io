# thornmgmt.com

One-page site for Thornhaven Capital. Plain HTML and one stylesheet. No build step, no
dependencies, no external requests — system fonts only, and the page loads nothing from a
third-party host.

## Layout

```
index.html        the page
404.html          not found
css/site.css      the whole stylesheet
CNAME             thornmgmt.com
.nojekyll         serve files verbatim, no Jekyll pass
```

## Editing

Open `index.html`. There is one screen of markup and one stylesheet. Colours and type stacks
are CSS custom properties at the top of `css/site.css`; the dark palette is the
`prefers-color-scheme` block directly beneath.

Preview by opening `index.html` in a browser, or serve the folder:

```
python -m http.server 8080
```

## Contact form

Posts to Formspree at `https://formspree.io/f/xgogpqdg`, delivering to
`manager@thornmgmt.com`.

The inline script keeps a guard: if the endpoint is ever reset to a `REPLACE_WITH`
placeholder, submission is blocked and visitors are pointed at the mailbox rather than
posting into the void.

Spam is handled by a `_gotcha` honeypot. There is deliberately no reCAPTCHA — it would add a
third-party request to a page that currently makes none.

## Search

`index.html` sends `robots: index, follow, nosnippet, max-image-preview:none`. The page is
findable, but Google shows only the firm name and the domain — no description line.

This is deliberate. The page carries too little prose for a search engine to summarise, so
left to itself Google composes a snippet from the visible text and drags in the form's field
labels and the honeypot's "leave this field empty". Removing the snippet is cleaner than
fighting over its contents, and it keeps the email address and phone number out of search
results.

Removing the `robots` meta reverts to a Google-composed snippet. If you ever do that, add a
real `description` first and mark the form region so its labels stay out.

## Deployment

GitHub Pages, served from `main` at the repository root.

DNS lives at GoDaddy on that registrar's own nameservers.

| Record | Value |
|---|---|
| `A @` | `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153` |
| `CNAME www` | `thornhaven-capital.github.io` |

Apex is primary; GitHub Pages redirects `www` to it.

**Google Workspace runs on this domain.** The 5 MX records, the SPF TXT, and the
`google-site-verification` TXT must never be touched. Only `A` and `CNAME` records change.

If the site appears to revert to the old GoDaddy parked page, that is browser cache, not DNS.
Check in a private window or on mobile data before changing anything.
