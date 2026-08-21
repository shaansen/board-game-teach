# The Teaching Shelf

Long-form briefings that teach a board game to someone who has **never played it**.

A rulebook tells you what the rules are. These pages tell you what the game *is*: why
each rule exists, what it feels like at the table, and which instincts will lose you
your first game.

**Live site:** https://shaansen.github.io/board-game-teach/

## What's here

| Path | What it is |
| --- | --- |
| `index.html` | The shelf — the landing page listing every briefing |
| `games/arkham-horror-lcg.html` | Arkham Horror: The Card Game — 15 points, complete |
| `games/spirit-island.html` | Spirit Island — 12 pieces, 1 written |
| `games/_template.html` | Starting point for a new briefing |
| `assets/dossier.css` | Shared layout system, for pages that want one |
| `assets/library.css` | Styles for the shelf |
| `.github/workflows/deploy.yml` | Publishes the repo to GitHub Pages on every push to `main` |

No build step, no dependencies, no framework. Plain HTML and CSS — open any file in a
browser and it works.

## Adding a game

1. `cp games/_template.html games/your-game.html` — or, if the game wants a look of
   its own, write a self-contained page with its own `<style>` block (that's what
   `spirit-island.html` does). Both are fine; see *Two ways to style a page* below.
2. Write it (see the house style below).
3. Add a card to the "On the shelf" list in `index.html`:

   ```html
   <a class="card" href="games/your-game.html">
     <span class="tab">Co-op · campaign</span>
     <h2>Your Game</h2>
     <p class="deck">The hook, in one italic sentence.</p>
     <div class="meta">
       <span><b>1–4</b> players</span>
       <span><b>~90 min</b></span>
       <span><b>12 of 12</b> points</span>
       <span><b>~20 min</b> read</span>
     </div>
     <span class="go">Read the briefing →</span>
   </a>
   ```

   Add `class="card t-yourgame"` and a `.t-yourgame{--card-accent:#...}` rule in
   `assets/library.css` if you want the card to carry the page's own accent colour,
   and a `<span class="status">In progress</span>` badge while it's unfinished.

4. Push to `main`. The workflow deploys it.

To preview locally: `python3 -m http.server` then open http://localhost:8000.

## House style

The thing that makes these work is the format, so keep it:

- **Numbered points, one idea each.** Each point is a `.page` section — a sheet of
  paper on a dark table. A reader should be able to stop after any point and still
  have learned something whole.
- **Order by dependency.** Point *n* only uses ideas from points 1…*n*−1. The first
  point is always "what kind of game is this and who are you playing against".
- **Explain the why.** Never "you get three actions" alone — always "you get three
  actions, it's never enough, and that's the game."
- **Second person, plain words.** No jargon before it's defined. Say "monster", not
  "non-player enemy unit".
- **End each point with a `.note`** — the one sentence worth remembering.
- **Finish with a "how not to lose your first game" point.** The instincts a normal
  board game trained into the reader are usually the ones that lose this one.

### Two ways to style a page

**Share the system.** Load `assets/dossier.css` and override a handful of CSS
variables — palette and typefaces only. Structure stays identical, so a reader who
learned one page can read them all. `arkham-horror-lcg.html` works this way.

**Bring your own.** If the game deserves a different shape on the page, write a
self-contained page with its own `<style>` block. `spirit-island.html` does this: a
vertical spine of numbered entries rather than a stack of dossier sheets. The only
things every page must share are the `← the shelf` backlink at the top, a footer link
back, and the house style below.

### The building blocks (shared system)

| Class | Use |
| --- | --- |
| `.page` | One numbered point |
| `.tab` | The point number badge |
| `.deck` | Italic standfirst under the heading |
| `.note` + `.lab` | Pull quote with a small caps label |
| `figure` + inline `<svg>` | Diagrams |
| `.scroll` around `<table>` | Keeps wide tables from breaking phones |

Diagrams are **inline SVG only** — no images, no libraries. Use the shared ink classes
(`f-neutral`, `f-teal`, `f-red`, `f-brass`, `f-violet`, `f-spent`) and text classes
(`tt`, `ts`) so figures look the same everywhere, and always give each `<svg>` a
`<title>` and `<desc>` for screen readers.

## Licence

Text and layout: do what you like with it. Game names, rules and settings belong to
their publishers — these pages are unofficial teaching material and reproduce no
copyrighted card text or art.
