# Textual-Vision
Textual Vision is intended to be used as a quick and token efficient way to pass visual data represented by text.

## GitHub Pages Static App

This repository ships a single-file static prototype (no build step) with two theme variants:

- **Retro (C64)**: `/` or `/retro/`
- **Modern (Cubism)**: `/modern/`

- The app runs entirely in-browser (no backend required).
- A Pages deploy workflow is included at `.github/workflows/deploy-pages.yml`.
- Enable **Settings → Pages → Build and deployment → Source: GitHub Actions**.

Once enabled, pushes to `main` will deploy the static web app.

## Using The Canvas

Open `/index.html` in a browser (or serve the repo locally with something like `python -m http.server`).

### Core Workflow
- Pick an **object type**, enter a **non-empty title**, pick a color, then **Draw** rectangles on the grid to create layout blocks.
- The title field is validated when drawing; empty titles are blocked with an inline error state.
- Click an existing block to **select** it and edit its title/code/color, duplicate it, delete it, or attach notes.
- Use **Ctrl/Cmd + Click** to select multiple elements for batch operations.
- Toggle **Allow Overlap** to permit stacked blocks (otherwise overlaps are blocked).
- When overlaps are enabled, use **Bring Front** / **Send Back** to control stacking order.
- Tip: `Alt` + click cycles through stacked elements under the cursor.

### Mouse Tools
- Use **Drag Element** and **Resize Element** tools for mouse-driven adjustments (with a ghost outline preview).
- Tip: `Esc` closes open modals/context menus, or cancels the current interaction.
- Most interactive controls include hover tooltips describing shortcuts and expected behavior.

### Visual Customization
- **Color Picker**: Choose from 9 predefined colors to visually distinguish different layout blocks.
- Each element can have its own color, making complex layouts easier to understand at a glance.
- Colors are preserved in YAML exports and reflected in PNG exports.

### Multi-Select & Alignment
- **Ctrl/Cmd + Click** to select multiple elements.
- When multiple elements are selected, alignment tools become available:
  - **← Align**: Align left edges
  - **Align →**: Align right edges
  - **⊞ Center**: Center horizontally
  - **↑ Align**: Align top edges
  - **Align ↓**: Align bottom edges
  - **⊟ Middle**: Center vertically
- Perfect for quickly organizing and aligning multiple blocks.
- Use **Merge to Same Object** to combine multiple selected blocks into one bounding-box element.

### Context Menu & Notes
- Right-click on a selected element to open a context menu with:
  - Add Note, Duplicate, Delete
  - Bring to Front, Send to Back
  - Alignment actions (for multi-select)
- Notes are saved with each element and persisted in YAML/local autosave state.

### Navigation
- Pan: middle mouse drag, or hold `Space` + left-drag
- Zoom: mouse wheel inside the viewport
- View tools: **Reset View** and **Fit**

### Keyboard Shortcuts
- `D`: draw mode
- `E`: erase mode (drag a box to delete all elements within)
- `F`: focus/center the selected element in the viewport
- `H` or `?`: show keyboard shortcuts help dialog
- `Esc`: cancel current draw / deselect / clear selection / clear tool
- `Delete` / `Backspace`: delete selected element(s) (disabled in text inputs)
- `Ctrl/Cmd+Z`: undo
- `Ctrl+Y` (or `Ctrl/Cmd+Shift+Z`): redo
- Arrow keys: nudge selected element (`Shift` = 5 cells)
- `Alt` + Arrow keys: resize selected element (`Shift` = 5 cells)
- **Note:** Hotkeys are disabled when typing in text inputs to prevent accidental actions

### Tool Selection
- **Clear Tool Buttons (X)**: Quickly clear the current tool selection and return to draw mode
- **Active Tool Highlighting**: The currently selected tool is visually highlighted
- **Mouse Tools**: Drag Element and Resize Element modes with ghost outline preview
- **Toggleable Tools**: All tools can be toggled on/off for better workflow control

## Storage & Export

### Autosave
- **Autosave (Local)** stores the canvas state in `localStorage` in your browser.
- Use **Clear Local Save** to remove it.

### Export Formats
- **Live ASCII** and **JSON** exports update as you edit.
- **Editable Exports**: Click the ✎ (pencil) button to enable edit mode for ASCII/JSON outputs
  - **ASCII Edit Mode**: Copy-only (does not modify the canvas); toggle off to return to live output
  - **JSON Edit Mode**: Manually edit canvas data; changes are validated and applied when you toggle edit off
  - **Validation**: Red border and error messages indicate invalid format
- **PNG Export**: Download a visual snapshot of your canvas as a PNG image file (preserves colors and layout).
- Toggle **Wrap Exports** to include (or omit) fenced code blocks in ASCII/JSON outputs.
- Use **Copy** buttons to copy ASCII/JSON/YAML to the clipboard.
- Use **Save As YAML** to download a full snapshot (including viewport transform and colors), and **Open File** to restore.
- Use **Paste YAML** to load a snapshot directly from a YAML string.
- You can also drag-and-drop a `.yaml`/`.yml` file (or YAML text) onto the viewport to load it.

### Element Search
- Use the **Search elements...** input to filter the elements list by label or code.
- Quickly find specific blocks in complex layouts.

### Help System
- Press `H` or `?` (or click the **Help** button) to open an interactive keyboard shortcuts reference.
- The help modal provides a comprehensive guide to all features and shortcuts.

### Themes & Settings
- Use the **Settings** gear to switch between Retro and Modern themes.
- Theme preference is saved in `localStorage` and is honored when loading the app root.
- Routing supports `/retro/` and `/modern/`, while `/` defaults to Retro unless a saved Modern preference exists.

### Logging
- Open **Settings → Show Logs** to view timestamped application logs (info/warn/error).
- **Comprehensive Logging**: All user actions, tool switches, and operations are logged
- **Error Handling**: Graceful error recovery with detailed error logging
- Use **Clear Logs** to reset the in-memory log stream and **Export Logs** to download a `.log` file.
- Logs help debug issues and track application behavior

## Advanced Features

### Enhanced Drawing & Selection
- **Visible Selection Rectangle**: Selection box is clearly visible while drawing
- **Erase as Inverse Draw**: Drag a box in erase mode to delete all elements within the selection
- **Active Tool Highlighting**: Currently selected tool is visually highlighted with border
- **Clear Tool Buttons**: Small X buttons to quickly clear tool selection

### View Controls
- **Fit All Elements**: New button to fit the entire grid in the viewport
- **Fit to Elements**: Existing fit button focuses on actual elements only
- **Reset View**: Return to default pan and zoom

## Notes

- The UI styling uses Tailwind via CDN; a network connection is required for the default styling when opened directly from disk.
- All features (colors, multi-select, search, alignment) are fully integrated with the undo/redo system.
- YAML save/load preserves all element properties including colors and positions.
