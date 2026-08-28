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
