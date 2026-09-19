# outline-site

The public web pages for **Outline**, an iPhone game. Three static pages, served
by GitHub Pages from `main` at the repository root.

| Page | Path | App Store Connect field |
|---|---|---|
| Landing | `/` | Marketing URL |
| Support | `/support/` | Support URL |
| Privacy policy | `/privacy/` | Privacy Policy URL |

HTML with one shared stylesheet derived from color tokens in the app's `Outline/Design/Palette.swift`
Edit a file, push to `main`, and Pages redeploys.

The support and privacy pages describe how the app actually behaves — local
storage only, Game Center for leaderboards, no analytics or tracking. If that
changes in the app, the privacy policy has to change with it, and its
"Last updated" date with it.

Feedback form: <https://forms.gle/3aU9ZnAmwT8JwQPE6>

## The App Clip association file

`.well-known/apple-app-site-association` is what lets iOS open Outline's App
Clip from a link on this site. iOS will not take our word for it: it fetches
that file itself, through Apple's own CDN, and opens the clip only if the file
names the clip's App ID. It has to sit at the **root** of whatever domain the
link is on, which is the reason this repository needs to be served from a
domain root rather than from a `/project-page/` subpath.

`_headers` exists for one line in it. The file has no extension, so a host will
usually guess `application/octet-stream`, and Apple wants `application/json`.
GitHub Pages cannot set headers at all, which is why it is not a viable host for
this; Cloudflare Pages and Netlify both read `_headers`.

Both files are inert on GitHub Pages — Jekyll drops paths beginning with `.` or
`_` — so they change nothing until the site moves.

After the first deploy to a host that serves them, check both halves:

```
curl -sI https://<host>/.well-known/apple-app-site-association | head -3
curl -s https://app-site-association.cdn-apple.com/a/v1/<host>
```

The first must be `200` with `application/json`. The second is Apple's own copy:
JSON means Apple has fetched and accepted the domain, `404` means it has not, and
that is the check that actually decides whether the clip can be invoked.

**There is deliberately no `applinks` key.** That key claims the domain's URLs
for the *installed* app, and Outline has no URL handling — no `onOpenURL`, no
`onContinueUserActivity`. Adding it would mean anyone with the app installed who
tapped a link to this site, including the privacy policy and support pages, would
launch Outline onto its home screen instead of reading the page. `applinks`
belongs in the same change as the code that handles the URL, not ahead of it.
