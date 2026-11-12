# Tide

Tide is [ChalkBored](https://chalkbored.win)'s web browser that runs inside one
page: tabs, an address bar, a home screen and settings, with sites opened through
the engine in `engine/` (see `engine/README.md`). It sends sites over a
[Wisp](https://github.com/MercuryWorkshop/wisp-protocol) connection through one of a
few public servers.

Live at **https://tide.guernica4u.workers.dev**. ChalkBored's Chalk TV loads it
there; Chalk Browser loads ChalkBored's own copy in `tide/`.

Tide began as a fork of [GUST](https://github.com/nautilus-os/GUST) by Nautilus
Labs. Since Tide 33 it is its own small page (`index.html`, about 40 KB) and has no
GUST code left.

## What it does

- **Tabs**, with each site's title and icon. They come back when Tide reopens,
  loading only when you open them.
- **Address bar and home screen**: type an address or a search. Settings picks
  DuckDuckGo, Google, Bing or Brave Search.
- **Bookmarks** (the star, or Ctrl+D) appear as letter tiles on the home screen.
  **History** lists every page visited. Both are under the ⋮ menu, and both are
  kept only in this browser. Fresh visits keep neither.
- **Reopen a closed tab** with Ctrl+Shift+T.
- **Skins**: Tide (all black), Firefox (light) and Chrome (dark).
- **Colours**: follow ChalkBored's look (Night, Mono, Space), pick one, or keep
  the skin's own.
- **Servers**: Tide starts on last time's fastest server and checks it in the
  background. Settings tests every server: each is pinged 3 times and must reach a
  real site. You can also pin one server.
- Links and windows that ask for a new tab open as Tide tabs. Pop-ups nobody
  clicked for are dropped.
- Site addresses are scrambled, so filters can't read which site is open.
- Inside another page it shows the theme's colour, a little see-through, instead
  of the picture.

## For the page around Tide

`index.html#tide=<JSON>`:

| Key | What |
|-----|------|
| `open` | a site (`https://…`) to show first |
| `ui: "tv"` | Chalk TV: just the site, no tabs or bar, downloads dropped |
| `fresh: true` | nothing from an earlier visit comes back (sites' storage and cookies, tabs) |
| `relay` | one of Tide's public servers, for this visit only |
| `look` | `night`, `mono` or `space` |

Once it can open sites, Tide posts `{tide: "ready"}` to its parent. It then takes
`{tide: "go", url}`, `{tide: "back"}`, `{tide: "reload"}` and `{tide: "look", look}`,
but only from ChalkBored's addresses (and `localhost` when Tide itself runs locally).
`_headers` lets only ChalkBored frame Tide.

## Download

Each [release](https://github.com/Guernica4u/Tide/releases) has a zip of the whole
site to put on your own static host.

## Running it

Serve the folder from any static host (`wrangler.jsonc` does this on Cloudflare).
Tide needs service workers, so it can't open sites in private windows.

## License

GNU Affero General Public License v3.0 (see `LICENSE`). The engine's parts and their
licenses are listed in `engine/README.md`. If you run a changed copy of Tide for
other people, you must offer them its source code.
