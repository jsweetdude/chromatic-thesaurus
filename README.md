# Chromatic Thesaurus

A zoomable map of color vocabulary for writers.

Hue runs left to right, red through violet and out to magenta. Lightness runs up and down: a word on the spectrum band is its hue at full strength, the tints float above it, the shades sink below. Whites, grays and blacks sit on a strip at the right. Every word carries a swatch, a one-line definition, real objects that wear the color, what it evokes on the page, where the word comes from, its three nearest neighbors, and a photograph fetched from Wikipedia when you look.

Single file, no build step. Open `index.html`.

## Using it

- Scroll or pinch to zoom, drag to pan, Shift + scroll to slide sideways. Zoom in and more words appear.
- Hover a word to preview it in the panel. Click to pin it. Esc unpins.
- Type in the search box to highlight matches; Enter jumps to the first one.
- Keyboard: Tab moves through the visible words, Enter pins. With the map focused, arrow keys pan, plus and minus zoom, zero resets.

## Editing the word list

The `WORDS` array at the top of the script in `index.html` is the data. One object per word:

| field | meaning |
|---|---|
| `n` | the word |
| `hex` | the swatch; position on the map is computed from it |
| `t` | tier: 1 shows at the widest zoom, 2 appears sooner, 3 only close in |
| `def` | one sentence: what the color is and how it differs from its neighbors |
| `obj` | real things of this color, as `[label, Wikipedia article title]` pairs; the first is the default photo |
| `ev` | what the color evokes |
| `or` | where the word comes from |
| `approx` | `true` when no conventional value exists and the swatch is a best guess |
| `neutral` | `true` to force a word onto the gray strip |
| `tags` | free labels, for example the book you met the word in |
| `found` | an optional note on where you met it |

Every Wikipedia title must be a real article with a lead image, or the card shows a placeholder.

## Notes

- Swatch values follow the common web conventions (Wikipedia, X11) where one exists. Words without one are flagged approximate in their card.
- Placement uses HSL hue for the horizontal axis and OKLab lightness for the vertical, relative to the lightness of the pure hue, so "above the band" always means paler than the basic color.
- Photos come from the Wikipedia page-images API at view time and are cached in the browser for a month. Nothing is stored server-side.
- Styling follows the A11y Context design system, dark theme by default, with a light theme toggle.
