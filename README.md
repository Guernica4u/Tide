# Tide

Tide is [ChalkBored](https://chalkbored.win)'s own copy of
[GUST](https://github.com/nautilus-os/GUST) by Nautilus Labs: a web browser that
runs inside one HTML page. It fetches sites with
[libcurl.js](https://github.com/ading2210/libcurl.js) (curl compiled to
WebAssembly) over a [Wisp](https://github.com/MercuryWorkshop/wisp-protocol)
WebSocket tunnel, rewrites them and shows them in a sandboxed frame. It needs no
service worker.

Live at **https://tide.guernica4u.workers.dev** (also https://study.chalkbored.win,
which school filters block along with all of .win), where ChalkBored's Chalk TV and
Chalk Browser load it.

## What Tide changes from GUST

- Starts from GUST's "Lite" settings (no tutorial, no ad-block panel, media
  viewers off, server settings hidden). They are defaults, so Settings changes stick.
- Removed: GUST's built-in chat-app client and its AI helper; the Opera GX skin
  from the pickers; Bing and Google search. Firefox is the default skin and
  DuckDuckGo the default search.
- One fixed storage namespace (`tide:`), since Tide is hosted at one address.
- **ChalkBored's server.** Opened as `https://study.chalkbored.win/#tide={"key":"…"}`,
  Tide uses `wss://tide.chalkbored.win/wisp/<key>/` and nothing else: no public
  relays, no fallback, and the key is kept in memory only (never saved). The
  address is removed from the URL bar as soon as it is read. Opened without a
  key, Tide uses public Wisp relays the way GUST does.
- **TV mode** for Chalk TV: `"ui":"tv"` hides tabs, the address bar and bookmarks,
  `"open":"<site>"` shows that site first, and the ChalkBored page around Tide can
  send `{tide:"go",url}`, `{tide:"back"}` and `{tide:"reload"}` (accepted only from
  ChalkBored). TV mode keeps its own tab, apart from the normal one.
- Works while framed inside another page (Chalk TV sits inside ChalkBored's
  Notebook): pages find Tide's window by a marker instead of `window.top`.
- `_headers` lets only ChalkBored frame Tide; `wrangler.jsonc` serves the repo
  as static files on Cloudflare.
- Says "Tide" and "tide" on screen.

## Running it

Open `index.html` in a browser, or serve the folder from any static host.

## Credits

Tide is GUST with changes, and all the hard work is GUST's:

| Who | What |
|-----|------|
| **lanefiedler** | Started GUST and built its original framework and UI |
| **dinguschan** | Maintained GUST and built most of its browser, features and fixes |
| **x8rr / hvtrs** | Ported GUST to SVG, documentation, testing |
| **Mercury Workshop** | The Wisp protocol |
| **ading2210** | libcurl.js |
| **Mozilla Foundation** | PDF.js |

## License

GNU Affero General Public License v3.0, the same as GUST (see `LICENSE`).
libcurl.js, bundled inside `index.html`, is under the GNU LGPL v3. If you run a
changed copy of Tide for other people, you must offer them its source code.
