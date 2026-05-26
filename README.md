# LIF — Sizzle Reel

A 13-scene narrative sizzle reel for **LIF (Love It Forward)** — built as a single self-contained HTML page with inline animation engines (chain reveal, dashboard counters, network-graph canvas, paper-grain backdrop).

## Run locally

```bash
npm install
npm start
```

Opens at `http://localhost:3000`. Use **← / →** or click the arrows to step through scenes.

## Files

| Path | What it is |
| --- | --- |
| `index.html` | The sizzle reel (deploy target). |
| `LIF Sizzle Revise.html` | Working copy — identical to `index.html`. |
| `fonts/` | Brand typefaces: Graphik · Apercu · Romana BT. |
| `package.json` | Runs `serve` as the static host. |
| `railway.json` | Tells Railway how to build & start. |

## Deploy to Railway from GitHub

1. **Push to GitHub.**
   ```bash
   git init
   git add .
   git commit -m "Initial LIF sizzle reel"
   git branch -M main
   git remote add origin git@github.com:<you>/<repo>.git
   git push -u origin main
   ```

2. **Create a Railway service.**
   - In Railway, *New Project → Deploy from GitHub repo*.
   - Pick this repo.
   - Railway detects `package.json`, installs `serve`, and runs `npm start`. It injects `PORT` automatically — the start script already binds to it.

3. **Generate a public domain.**
   - In the service's *Settings → Networking*, click *Generate Domain*. That's it.

No env vars required.

## How the reel works

- **13 scenes**, defined as a single `var scenes = [...]` array in `index.html`. Each entry has `{bg, lt, dur, en, lv, html}`.
- **Engines** are inline JS hooked by the `en` field:
  - `chain` — staggered SVG node + line reveal (Scene 4).
  - `dash` — animated metric counters (Scene 7).
  - `osnet` — full-screen network graph with progressive brand-node reveal and recursive pulse propagation (Scene 12). `lv: 'osnetstop'` halts it on exit.
- **Navigation**: ← / → keys, spacebar to advance, or the on-screen arrows. State is reset cleanly between scenes.

## Editing copy

Each scene's HTML lives inline in the `scenes` array. Open `index.html`, find the `var scenes=[` block (~line 269), edit the relevant string. All scene strings use single quotes; escape any apostrophes as `\'`.
