# Textual-Vision
Textual Vision is intended to be used as a quick and token efficient way to pass visual data represented by text.

## GitHub Pages Static App

This repository now ships a single-file static prototype at `/index.html` for a **C64-themed Visual-to-Text Ideation Canvas**.

- The app runs entirely in-browser (no backend required).
- A Pages deploy workflow is included at `.github/workflows/deploy-pages.yml`.
- Enable **Settings → Pages → Build and deployment → Source: GitHub Actions**.

Once enabled, pushes to `main` will deploy the static web app.

## Using The Canvas

Open `/index.html` in a browser (or serve the repo locally with something like `python -m http.server`).

**Core workflow**
- Pick a label, then **Draw** rectangles on the grid to create layout blocks.
- Click an existing block to **select** it and edit its label/code, duplicate it, or delete it.
- Toggle **Allow Overlap** to permit stacked blocks (otherwise overlaps are blocked).
- When overlaps are enabled, use **Bring Front** / **Send Back** to control stacking order.
- Tip: `Alt` + click cycles through stacked elements under the cursor.

**Navigation**
- Pan: middle mouse drag, or hold `Space` + left-drag
- Zoom: mouse wheel inside the viewport
- View tools: **Reset View** and **Fit**

**Shortcuts**
- `D`: draw mode
- `E`: erase mode
- `F`: focus/center the selected element in the viewport
- `Esc`: cancel current draw / deselect
- `Delete` / `Backspace`: delete selected element
- `Ctrl/Cmd+Z`: undo
- `Ctrl+Y` (or `Ctrl/Cmd+Shift+Z`): redo
- Arrow keys: nudge selected element (`Shift` = 5 cells)
- `Alt` + Arrow keys: resize selected element (`Shift` = 5 cells)

## Storage & Export

**Autosave**
- **Autosave (Local)** stores the canvas state in `localStorage` in your browser.
- Use **Clear Local Save** to remove it.

**Exports**
- Live **ASCII** and **JSON** exports update as you edit.
- Toggle **Wrap Exports** to include (or omit) fenced code blocks in ASCII/JSON outputs.
- Use **Copy** buttons to copy ASCII/JSON to the clipboard.
- Use **Save As YAML** to download a full snapshot (including viewport transform), and **Open File** to restore.
- Use **Paste YAML** to load a snapshot directly from a YAML string.
- You can also drag-and-drop a `.yaml`/`.yml` file (or YAML text) onto the viewport to load it.
- Use **Copy YAML** to copy the full YAML snapshot to the clipboard.

## Notes

- The UI styling uses Tailwind via CDN; a network connection is required for the default styling when opened directly from disk.
