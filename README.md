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

## Fixing a chord shape

Fret maps come from a search in `public/index.html`. To override a shape the search gets wrong, add an entry to `CORNER_CASES` (frets listed from string 6 to 1, `null` = muted):

```js
{ root: "E", rootStr: 6, chord: "maj7", thirdPos: "up3", frets: [0, 2, 1, 1, 0, 0] },
```
