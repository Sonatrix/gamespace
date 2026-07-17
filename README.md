# 🎪 GameSpace — Learning Games for Kids

**17 free, kid-friendly learning games for ages 2–8.** No ads, no tracking, no downloads — every game is a single self-contained HTML file that works offline in any modern browser.

**▶ Play now:** https://sonatrix.github.io/gamespace/

![Ages 2-8](https://img.shields.io/badge/ages-2%E2%80%938-ff6b8a) ![No dependencies](https://img.shields.io/badge/dependencies-none-58b368) ![Works offline](https://img.shields.io/badge/works-offline-4ea8de) ![License](https://img.shields.io/badge/license-MIT-b58cf0)

## 🕹️ The Games

| Game | Ages | Teaches |
|---|---|---|
| 🐰 [Bunny Hop](bunny-hop.html) | 4–7 | Timing & motor skills — jump over friendly obstacles |
| 🔷 [Shape Sorter](shape-sorter.html) | 2–4 | Shapes & colors — match holes, sort into buckets |
| 🍎 [ABC Talking Friends](abc-talking-friends.html) | 2–5 | Alphabet & phonics — every letter speaks |
| 🎨 [Coloring Book](coloring-book.html) | 2+ | Creativity — tap-to-fill coloring pages |
| 🃏 [Memory Match](memory-match.html) | 2–6 | Visual memory — find the pairs, 4 decks |
| 🎹 [Music Maker](music-maker.html) | 2–7 | Music — do-re-mi piano, learn real songs |
| 🔥 [Matchstick Math](matchstick-math.html) | 3–5 | *How* counting, adding & taking away work |
| 🎉 [Pattern Party](pattern-party.html) | 3–6 | Logic — what comes next? |
| 🔢 [Dot to Dot](dot-to-dot.html) | 3–6 | Number order — connect dots, reveal pictures |
| 🦉 [Simon the Owl](simon-owl.html) | 3–7 | Listening memory — repeat the growing tune |
| 👀 [Odd One Out](odd-one-out.html) | 3–6 | Categorization — find what doesn't belong, hear why |
| ✏️ [Trace & Write](trace-and-write.html) | 3–6 | Handwriting — rainbow-brush letters & numbers |
| 🧱 [Word Builder](word-builder.html) | 4–6 | Spelling — build CAT, DOG, FISH with phonics |
| 🗺️ [Maze Explorer](maze-explorer.html) | 4–8 | Spatial thinking — 5 themed lands, growing mazes |
| 🎈 [Balloon Pop Math](balloon-pop-math.html) | 5–8 | Arithmetic — addition, subtraction, times tables |
| 🏪 [Little Shop](little-shop.html) | 5–8 | Money — pay exact amounts with coins |
| 🕐 [What Time Is It?](clock-time.html) | 5–8 | Telling time — o'clock, half past, quarters |

Together they cover the full early-learning arc: **motor skills → shapes & colors → counting → letters → spelling → writing → arithmetic → money & time**, plus memory, logic, music and creative free play.

## ✨ Design Principles

- **No fail states.** Wrong answers wiggle gently and get an encouraging hint. Nothing dies, nothing games-over, no timers pressure the child.
- **Voice narration everywhere.** Built-in browser speech (Web Speech API) reads prompts, counts along, and sounds out phonics — so pre-readers can play unassisted. Toggle with 🗣️.
- **Music & sound with zero audio files.** Every melody, chime and cha-ching is synthesized live with WebAudio. Each game has its own theme tune, toggleable with 🎵 / 🔊.
- **Big targets, gentle pacing.** Chunky buttons, generous hitboxes, coyote-time jumps — designed for little hands on tablets.
- **Stars and confetti, not scores and losses.** Positive reinforcement only.

## 🚀 Run It

No build step, no dependencies. Any of these works:

```bash
# just open a file
open index.html            # macOS
start index.html           # Windows

# or serve the folder
npx serve .
python -m http.server
```

> Tip: voice narration sounds best in Chrome or Edge, which ship with the best built-in voices.

## 🔧 Customize

Every game has a `CONFIG` object (and data tables) at the top of its script — tweak difficulty, speeds, colors, word lists, songs and melodies without touching the game logic. Examples:

- `word-builder.html` → add words to `WORDS` (`['fox','🦊']` — they just work)
- `music-maker.html` → add songs to `SONGS` as sequences of key indices
- `maze-explorer.html` → adjust `startSize`/`maxSize`, or add a whole new themed land in `THEMES`
- `abc-talking-friends.html` → swap any letter's word/emoji in `LETTERS`

## 📁 Structure

```
gamespace/
├── index.html        ← landing page (SEO meta, sitemap-linked)
├── <game>.html       ← 17 self-contained games (HTML+CSS+JS each)
├── robots.txt
├── sitemap.xml
└── README.md
```

## 🌐 Deploy

Push to GitHub, then enable **Settings → Pages → Deploy from branch → main / (root)**. The site is fully static and each page is standalone, so it also works on Netlify, Vercel, or any plain file server.

---

Made with ❤ for little learners. Built with [Claude Code](https://claude.com/claude-code).
