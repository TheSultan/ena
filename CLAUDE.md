# CLAUDE.md

## What This Is

Small web games for Ena (dad's daughter, ~4.5 years old). They play together over Zoom screenshare — dad clicks everything since Ena can't control the screen yet. All games are cooperative, not competitive, and must be explainable in one sentence to a 4-year-old.

## Repo Structure

```
index.html          ← homepage linking all games
tictactoe/          ← Tic Tac Toe with MLP character symbols
  images/           ← 10 PNG character images (shared by all games)
memory/             ← Memory matching card game (5×4 grid, 10 pairs)
counting/           ← Count the ponies (1–10, 3 multiple choice answers)
spinner/            ← Spin-the-wheel random character picker
stickers/           ← Drag-and-drop sticker scene builder
storybook/          ← 7-page illustrated story ("A Magical Day in Ponyville")
```

## Shared Assets

All games use the same 10 character PNGs stored in `tictactoe/images/`. Reference them with relative path `../tictactoe/images/[name].png`. The images are downloaded locally — do NOT hotlink from Fandom/wikia CDN (their CDN blocks requests with third-party Referer headers, which breaks GitHub Pages).

Characters and filenames:
- twilight.png, luna.png, celestia.png, applejack.png, sunset.png
- starlight.png, trixie.png, fluttershy.png, rarity.png, cadance.png

## Design Constraints

- **Single-file HTML/CSS/JS** — no frameworks, no build step, no npm
- **Dad clicks for Ena** — Ena directs verbally over Zoom. This drives the labeling pattern:
  - Grid coordinates (A–D rows, 1–5 columns) on memory cards
  - A/B/C labels on counting game answer buttons
  - Row/column labels on tic-tac-toe board
- **Cooperative** — celebrate success together, no winner/loser between Ena and dad
- **Confetti** on correct answers and wins (`spawnConfetti()` is in every game)
- **GitHub Pages** deploys from `main` branch automatically

## Deployment

Push to `main` → GitHub Pages auto-deploys. If Pages seems stale after a push, force a rebuild with an empty commit: `git commit --allow-empty -m "trigger rebuild"`.

