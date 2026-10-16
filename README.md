# Movable Guitar Shell & Inversion Explorer

A single static page (`public/index.html`) that shows a chord's fret map from the root note, the root string, the position of the 3rd and the chord type.

## Serve locally

The page has no build step and no dependencies. Pick one:

**Wrangler (same setup as the Cloudflare deploy, needs Node.js)**
```
npx wrangler dev
```
Open http://localhost:8787

**Python**
```
python -m http.server 8000 -d public
```
Open http://localhost:8000

**Node.js without Wrangler**
```
npx serve public
```
Open the URL it prints (usually http://localhost:3000)

You can also open `public/index.html` directly in a browser, since the page loads nothing else.

## Deploy

Pushing to `main` deploys to Cloudflare Workers using `wrangler.jsonc`, which serves `./public` as static assets. In the Cloudflare build settings, leave the build command empty and set the deploy command to `npx wrangler deploy`.

## Chord naming

Chords are named `<root><suffix> on <root string>`, for example `G on 4`, `Em7 on 6` or `C9 on 5`.

| Suffix | Chord type | Example |
|---|---|---|
| *(none)* | Major | `G on 4` |
| `m` | Minor | `Em on 5` |
| `maj7` | Major 7 | `Cmaj7 on 5` |
| `m7` | Minor 7 | `Em7 on 6` |
| `7`, `9`, `11`, `13` | Dominant 7 / 9 / 11 / 13 | `C9 on 5` = Dom 9 |
| `/<bass>` | Major with its 6th in the bass | `C/A on 5` |

A bare number always means a dominant chord: `C9` is a Dom 9 (3, b7, 9), not a major 9.

## Fixing a chord shape

Fret maps come from a search in `public/index.html`. To override a shape the search gets wrong, add an entry to `CORNER_CASES` (frets listed from string 6 to 1, `null` = muted):

```js
{ root: "E", rootStr: 6, chord: "maj7", thirdPos: "up3", frets: [0, 2, 1, 1, 0, 0] },
```
