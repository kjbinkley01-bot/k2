# k2

## PlateCraft

A browser-based 3D modeler built around 3D printing instead of engineering CAD.

- **Build with shapes:** add boxes, cylinders, cones, spheres, hex prisms and wedges, and drag, rotate and resize them on the build plate. Any shape can be a **hole**. Shapes are applied top to bottom in the list, so a hole cuts everything above it.
- **Templates with sliders:** dice tower, card deck box, hex terrain tiles, miniature bases, controller/phone stand and cable organizer. Change the sliders, then edit the shapes by hand if you want.
- **Print check:** live warnings for overhangs that need supports, flat ceilings, thin walls (based on your nozzle), pieces floating in mid-air, a small footprint, and models that don't fit your printer. The check view makes clean surfaces see-through so problems inside the model still show.
- **Auto-orient:** tries six orientations and picks the one that needs the least support.
- **Filament estimate:** weight, length and cost for your material and infill.
- **Export:** a watertight binary STL, built with [manifold](https://github.com/elalish/manifold), ready for any slicer.

### Run it locally

The geometry engine loads a WebAssembly file, so serve the folder instead of opening the file directly:

```sh
cd platecraft
python3 -m http.server 8000
# open http://localhost:8000
```

An internet connection is needed for Three.js, manifold.js and the fonts (loaded from jsDelivr and Google Fonts). `manifold.wasm` is included in the folder (Apache-2.0, see `MANIFOLD_LICENSE`).

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

### Ideas for next steps

- Text and embossed labels
- Rounded edges / fillets
- Gridfinity bins
- 3MF export with colors
- Import an STL to modify
- Layer-by-layer preview slider
