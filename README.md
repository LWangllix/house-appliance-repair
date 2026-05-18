# Rimas Vanglikas — buitinės technikos remontas

Vienfailis statinis landing puslapis (`index.html`). Talpinama GitHub Pages.

## Greitas deploy į GitHub Pages (per Claude Code)

Atsidaryk šitą aplanką su Claude Code ir paprašyk:

> Sukurk viešą GitHub repo `rimas-vanglikas`, push'ink šį aplanką į `main` šaką ir įjunk GitHub Pages iš `main` šakos root direktorijos. Po to grąžink man tiesioginį URL.

Arba paleisk pats terminale (reikia [GitHub CLI](https://cli.github.com/) — `gh`):

```bash
cd deploy
git init -b main
git add .
git commit -m "Initial site"
gh repo create rimas-vanglikas --public --source=. --remote=origin --push
gh api -X POST "repos/$(gh repo view --json nameWithOwner -q .nameWithOwner)/pages" \
  -f "source[branch]=main" -f "source[path]=/"
```

Po ~1 min puslapis bus pasiekiamas adresu:
`https://<tavo-github-username>.github.io/rimas-vanglikas/`

## Custom domeną (pvz. `rimasvanglikas.lt`)

1. Repo `Settings → Pages → Custom domain` — įvesk domeną.
2. Pas registratoriaus DNS:
   - `A` įrašai → `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - arba `CNAME` `www` → `<tavo-username>.github.io`
3. Įjunk „Enforce HTTPS".

## Vietinis testavimas

Tiesiog atidaryk `index.html` naršyklėje, arba:

```bash
python3 -m http.server 8000
# http://localhost:8000
```

## Redagavimas

Visa logika viename `index.html` — HTML + CSS + minimalus JS scroll animacijoms. Šriftai (Space Grotesk, Instrument Serif, JetBrains Mono) kraunami iš Google Fonts CDN.

Pakeitimui: redaguok `index.html`, commit'ink, push'ink — GitHub Pages atsinaujins per ~30 s.
