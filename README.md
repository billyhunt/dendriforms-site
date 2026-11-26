# dendriforms.ai

One static page. No build step, no dependencies, no outside scripts.

| File | What it is |
|---|---|
| `index.html` | The whole site. Styles are inline. |
| `fonts/` | Archivo, Archivo Black and DM Mono (Latin subset), with their SIL Open Font License texts. |
| `favicon.svg` | The icon. |
| `.github/workflows/deploy.yml` | Publishes `main` to AWS on every push. |
| `DEPLOY.md` | How the site is published and tested. Start there. |

View it locally:

```sh
python3 -m http.server 8000
```

Then open <http://localhost:8000>.
