# outline-site

The public web pages for **Outline**, an iPhone game. Three static pages, served
by GitHub Pages from `main` at the repository root.

| Page | Path | App Store Connect field |
|---|---|---|
| Landing | `/` | Marketing URL |
| Support | `/support/` | Support URL |
| Privacy policy | `/privacy/` | Privacy Policy URL |

Hand-written HTML with one shared stylesheet — no build step, no dependencies.
Edit a file, push to `main`, and Pages redeploys.

## Keeping it honest

`assets/site.css` transcribes the colour tokens from the app's
`Outline/Design/Palette.swift`. The app is the source of truth; if the palette
moves there, move it here.

The support and privacy pages describe how the app actually behaves — local
storage only, Game Center for leaderboards, no analytics or tracking. If that
changes in the app, the privacy policy has to change with it, and its
"Last updated" date with it.

Feedback form: <https://forms.gle/3aU9ZnAmwT8JwQPE6>

## Local preview

```bash
python3 -m http.server 8000
```

Then open <http://localhost:8000/>.
