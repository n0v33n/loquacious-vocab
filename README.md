# Loquacious Vocab

A fast, categorized GRE vocabulary reference — **725 words** across **35
themed categories**, plus a **root‑words** reference at the bottom of the
page. Every word can be **clicked to hear it pronounced**, and **hovering**
(or tapping the ⓘ on mobile) pops up a **flashcard** with the full
definition, an example sentence, and a memory‑aid **mnemonic** where one
exists (227 of the words have a mnemonic).

Two files, no build step, no framework, no dependencies:
- `index.html` — the whole site (HTML/CSS/vanilla JS)
- `data.json` — the word, category, and root‑word data it loads

## Features
- **Total word count** always visible in the header, plus a live "shown"
  count as you filter.
- **Category chips** — tap a chip to filter to just that theme (only
  categories with words in them are shown, each with a live count).
- **Search** — matches word, synonym, or definition text, with live
  highlighting.
- **Click‑to‑pronounce** — uses the browser's built‑in `speechSynthesis`
  API, so it works offline with no API key.
- **Hover flashcard** — hovering any word card (desktop) or tapping its ⓘ
  icon (touch devices) shows a flashcard with the definition, an example
  sentence, and the mnemonic.
- **Root words** — a dedicated section at the end of the page listing
  common Latin/Greek roots (e.g. `circum-`, `voc-`, `ex-`) with their
  meaning and clickable example words drawn from the list above.
- Built with system fonts + Google Fonts (Fraunces/Inter/IBM Plex Mono),
  no client‑side framework, so it loads instantly and scrolls smoothly
  even on a phone.

## Run locally
Just open `index.html` in a browser — or, since it `fetch`es `data.json`,
serve it locally so that request works (opening the file directly with
`file://` will fail the fetch in most browsers):
```bash
cd loquacious-vocab
python3 -m http.server 8080
# visit http://localhost:8080
```

## Step-by-step: push to GitHub
1. **Create a new, empty repository** on GitHub (no README/license, so it's
   truly empty): go to https://github.com/new, name it e.g.
   `loquacious-vocab`, and click **Create repository**.
2. On your computer, open a terminal in the folder that contains
   `index.html`, `data.json`, and this `README.md`.
3. Initialize git and make the first commit:
   ```bash
   git init
   git add .
   git commit -m "Loquacious Vocab: GRE word bank"
   git branch -M main
   ```
4. Connect it to the GitHub repo you just created and push:
   ```bash
   git remote add origin https://github.com/<your-username>/loquacious-vocab.git
   git push -u origin main
   git remote add remo https://github.com/n0v33n/loquacious-vocabs.git
   git push -u remo main
   ```
   (GitHub will show you this exact command on the empty repo's page —
   you can copy it from there instead of retyping your username.)

## Step-by-step: deploy on Vercel
1. Go to **https://vercel.com/new** and sign in with your GitHub account
   if you haven't already (Vercel will ask for permission to see your
   repos — you can limit it to just this one).
2. Find `loquacious-vocab` in the list and click **Import**.
3. On the configuration screen:
   - **Framework Preset:** choose **Other** (this is a static site — no
     build command and no output directory are needed).
   - Leave the *Build Command* and *Output Directory* fields empty/default.
4. Click **Deploy**. Vercel builds and deploys in a few seconds and gives
   you a live URL like `https://loquacious-vocab.vercel.app`.
5. That's it — every future `git push` to `main` automatically triggers a
   new deployment on the same URL. To use a custom domain, go to the
   project's **Settings → Domains** in Vercel and add it there.

## Adding more words
Open `data.json` and add an object to the `words` array. `mnemonic` and
`example` are optional — leave them out (or set to `""`) if you don't have
one yet:
```json
{
  "word": "sedulous",
  "equivalents": "diligent, assiduous",
  "meaning": "showing dedication and diligence",
  "category": "diligence",
  "example": "Her sedulous attention to detail caught every typo.",
  "mnemonic": "\"assiduous\" sounds like it — both mean hard-working."
}
```
`category` must match one of the `id`s listed in the `categories` array at
the top of the file. To add a brand-new category, add
`{ "id": "yourid", "title": "Your Title / Here" }` to that array first.

## Adding root words
Add an object to the `roots` array:
```json
{ "root": "bene-", "meaning": "good", "examples": ["benevolent", "beneficent"] }
```
Each string in `examples` should be the exact spelling of a word that
already exists in the `words` array, so it can be clicked to hear it
pronounced and to pop open its flashcard.
