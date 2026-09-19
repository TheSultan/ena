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
zingo/              ← Zingo: cooperative bingo, fill a 3×3 card from two-tile pulls
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

## Mobile

Every game and the homepage must work at phone width (~375px) as well as desktop. Check new or changed pages in a 375px-wide frame before committing.

- Keep `<meta name="viewport" content="width=device-width, initial-scale=1.0">` and `touch-action: manipulation` on `body`
- No fixed pixel widths for boards, scenes, or canvases. Use `width: 100%` with a `max-width`, `aspect-ratio`, and `minmax(0, 1fr)` grid columns
- Position things inside scaled scenes with percentages (or `cqw` units for text), not pixels
- Never put `overflow: hidden` on `body`, so long content can scroll
- Add a `@media (max-width: 600px)` block that shrinks headings, padding, gaps, and labels
- Keep the A/B/C and row/column labels visible on mobile
- Headless Chrome won't go below ~500px wide, so test by loading the page in a 375px iframe (see the verify skill)

## Deployment

Push to `main` → GitHub Pages auto-deploys. If Pages seems stale after a push, force a rebuild with an empty commit: `git commit --allow-empty -m "trigger rebuild"`.

