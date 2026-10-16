# k2

## PlateCraft

A browser-based 3D modeler built around 3D printing instead of engineering CAD, tuned for a **Voxelab Aries** (200 × 200 × 200 mm, 0.4 mm nozzle, glass bed).

- **Build with shapes:** boxes, cylinders, cones, spheres, hex prisms and wedges you drag, rotate and resize on the build plate. Any shape can be a **hole**. Shapes apply top to bottom in the list, so a hole cuts everything above it.
- **Templates with sliders:** dice tower, card deck box, hex terrain tiles, miniature bases, controller/phone stand and cable organizer.
- **Import STL:** open or drag in any watertight STL (from Printables, Thingiverse, etc.), then scale it, combine it with shapes, check it or split it.
- **Print check:** overhangs that need supports, flat ceilings, thin walls for your nozzle, pieces floating in mid-air, small footprints, models too big for the printer, and material warnings for the Aries (e.g. ABS curling). The check view makes clean surfaces see-through so hidden problems show.
- **Split & plates:** cuts a model that is too big into pieces that fit, using as few pieces as possible. It also:
  - adds alignment pin holes (printed pins, 1.75 mm filament pieces, or wood/metal dowels),
  - engraves matching joint numbers on both cut faces,
  - orients each piece for the least support,
  - packs pieces onto 200 × 200 plates,
  - exports one STL per plate, one per piece, and an `ASSEMBLY.txt` guide with per-plate filament and time estimates.
- **Suggested settings** for PLA, PETG, ABS, ASA and TPU, with Aries-specific tips (PTFE hotend limit, paper leveling, glass bed).
- **Works with Claude:** see below.
- **Filament estimate:** weight, length, cost and rough print time.

### Working with Claude

PlateCraft reads a small JSON **recipe** format that Claude can write. There are three ways to use it, all in the **Claude** tab:

1. **Describe a model** (on the hosted page): type what you want, and Claude builds it on the plate. Tick "Change the current model" to edit what's there instead.
2. **Paste a recipe** from any Claude chat. Use **Copy format guide** to teach a new chat the format, and **Copy model for Claude** to send your current model plus its print-check notes for changes.
3. **Sent from Claude:** in a Claude Code session, ask Claude to "send a model to PlateCraft". Claude writes it into the page's `inbox` collection and it appears in the list, ready to open.

The recipe format, briefly (the full guide is built into the app):

```json
{"platecraft": 1, "name": "Coaster", "parts": [
  {"shape": "cylinder", "size": [90, 90, 5], "at": [0, 0, 2.5]},
  {"shape": "cylinder", "size": [82, 82, 2], "at": [0, 0, 5], "hole": true}
]}
```

- **Shapes:** `box`, `cylinder`, `cone`, `sphere`, `hex`, `wedge`, `extrude` (2D outline + height), `revolve` (profile spun around Z), `text` (block letters).
- **Units:** millimetres, Z up, plate at z = 0.
- `at` is the centre of the part's bounding box, and `rotate` is in degrees.

An inbox document looks like `{"name": "...", "note": "...", "createdAt": "<ISO time>", "recipe": { ...recipe... }}`.

### Run it locally

The geometry engine loads a WebAssembly file, so serve the folder instead of opening the file directly:

```sh
cd platecraft
python3 -m http.server 8000
# open http://localhost:8000
```

An internet connection is needed for Three.js, manifold.js and the fonts (loaded from jsDelivr and Google Fonts). `manifold.wasm` is included in the folder (Apache-2.0, see `MANIFOLD_LICENSE`). Locally, single STLs download directly. On the hosted page they arrive inside a .zip, because hosted pages can't offer .stl files directly. Describe-a-model and the inbox only work on the hosted page.

### Keyboard

| Key | Action |
| --- | --- |
| T / R / S | Move / rotate / resize gizmo |
| H | Toggle solid / hole |
| B | Drop the selected shape onto the plate |
| Delete | Delete the selected shape |
| Ctrl+D | Duplicate |
| Ctrl+Z / Ctrl+Shift+Z | Undo / redo |
| Esc | Deselect |
