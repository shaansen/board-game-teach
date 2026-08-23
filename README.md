# The Teaching Shelf

Long-form briefings that teach a board game to someone who has **never played it**.

A rulebook tells you what the rules are. These pages tell you what the game *is*: why
each rule exists, what it feels like at the table, and which instincts will lose you
your first game.

**Live site:** https://shaansen.github.io/board-game-teach/

## What's here

| Path | What it is |
| --- | --- |
| `index.html` | The shelf, the landing page listing every briefing |
| `games/arkham-horror-lcg.html` | Arkham Horror: The Card Game, 15 points, complete |
| `games/spirit-island.html` | Spirit Island, 12 pieces, complete |
| `games/troyes.html` | Troyes, 14 chapters, complete |
| `games/aeons-end.html` | Aeon's End, 10 points, complete |
| `games/obsession.html` | Obsession, 22 points, complete |
| `games/paperback.html` | Paperback, 10 points, complete |
| `games/_template.html` | Starting point for a new briefing |
| `assets/dossier.css` | Shared layout system, for pages that want one |
| `assets/library.css` | Styles for the shelf |
| `.github/workflows/deploy.yml` | Publishes the repo to GitHub Pages on every push to `main` |

No build step, no dependencies, no framework. Plain HTML and CSS: open any file in a
browser and it works.

## Adding a game

1. `cp games/_template.html games/your-game.html`, or, if the game wants a look of
   its own, write a self-contained page with its own `<style>` block (that's what
   `spirit-island.html` and `troyes.html` do). Both are fine; see *Two ways to style
   a page* below.
2. Write it (see the house style below).
3. Add a card to the shelf in `index.html`. First an emblem `<symbol>` in the icon
   set at the top, then a box:

   ```html
   <a class="game" href="games/your-game.html" style="--accent:#7A241E">
     <span class="emblem"><svg><use href="#e-yourgame"/></svg></span>
     <h3>Your Game</h3>
     <p class="hook">The hook, in one sentence.</p>
   </a>
   ```

4. Push to `main`. The workflow deploys it.

To preview locally: `python3 -m http.server` then open http://localhost:8000.

## House style

The thing that makes these work is the format, so keep it:

- **Numbered points, one idea each.** Each point is a `.page` section, a sheet of
  paper on a dark table. A reader should be able to stop after any point and still
  have learned something whole.
- **Order by dependency.** Point *n* only uses ideas from points 1…*n*−1. The first
  point is always "what kind of game is this and who are you playing against".
- **Explain the why.** Never "you get three actions" alone, always "you get three
  actions, it's never enough, and that's the game."
- **Second person, plain words.** No jargon before it's defined. Say "monster", not
  "non-player enemy unit".
- **End each point with a `.note`**: the one sentence worth remembering.
- **Finish with a "how not to lose your first game" point.** The instincts a normal
  board game trained into the reader are usually the ones that lose this one.

### Two ways to style a page

**Share the system.** Load `assets/dossier.css` and override a handful of CSS
variables, palette and typefaces only. Structure stays identical, so a reader who
learned one page can read them all. `arkham-horror-lcg.html` works this way.

**Bring your own.** If the game deserves a different shape on the page, write a
self-contained page with its own `<style>` block. `spirit-island.html` is a vertical
spine of numbered entries; `troyes.html` is a parchment chronicle with a cathedral
progress bar; `aeons-end.html` is a run of glowing breaches in the Void;
`obsession.html` is a single card you deal through from a servants' bell board;
`paperback.html` is a stack of pulp novels on a shelf; `glass-road.html`
reveals one point at a time and hands you two working production wheels to spin.
The only things every page must share are the `← the shelf` backlink at the top, a footer link back, and the house style below.

### The building blocks (shared system)

| Class | Use |
| --- | --- |
| `.page` | One numbered point |
| `.tab` | The point number badge |
| `.deck` | Italic standfirst under the heading |
| `.note` + `.lab` | Pull quote with a small caps label |
| `figure` + inline `<svg>` | Diagrams |
| `.scroll` around `<table>` | Keeps wide tables from breaking phones |

Diagrams are **inline SVG only**: no images, no libraries. Use the shared ink classes
(`f-neutral`, `f-teal`, `f-red`, `f-brass`, `f-violet`, `f-spent`) and text classes
(`tt`, `ts`) so figures look the same everywhere, and always give each `<svg>` a
`<title>` and `<desc>` for screen readers.

## Licence

Text and layout: do what you like with it. Game names, rules and settings belong to
their publishers. These pages are unofficial teaching material and reproduce no
copyrighted card text or art.
