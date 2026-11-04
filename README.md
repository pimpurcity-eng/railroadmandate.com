# railroadmandate.com

The game's website. One static page (`index.html`), images in `img/`, the game's own fonts (Lora, Oswald) in `fonts/`. No build step.

- Preview: `cd site && python3 -m http.server 8765`, then open http://localhost:8765 (fonts need http, not file://).
- Every picture is either a real capture from the game (`3d_*`, `ph_*`) or Matthew's art from `game/art` (converted to webp).
- To refresh the 3D shots, use the capture flags in HANDOFF section 8 with `--hide-ui=1 --resolution 1600x900`.
- `CNAME` holds the domain. Hosting: GitHub Pages from a **public** repo (Pages on a private repo needs a paid plan).

## Play in your browser (`play/`)

- `tools/build_web.sh` exports the Web preset (Compatibility renderer, no threads, so GitHub Pages needs no special headers), gzips the game data and splits it into 26 MB `pack-*.bin` parts (GitHub refuses files over 100 MB). `play/index.html` downloads the parts, unpacks them in the browser (DecompressionStream) and starts Godot with `--main-pack game.pck`.
- The build files are git-ignored here; they live only in the `railroadmandate.com` repo.
- Publish: run `tools/build_web.sh`, copy everything in `site/` (keep that repo's `CNAME`) into a clone of `pimpurcity-eng/railroadmandate.com`, commit, push. Pages redeploys in a minute or two.
- The web build has no system fonts, so symbols (▸ ♪ ☰ ✓) come from `game/assets/fonts/Symbols.ttf`, a DejaVu subset set as every theme font's fallback in `rail_theme.gd`. If you add a new symbol to the UI, add it to that subset.
