# SpriteSheetCutter

A lightweight, zero-build, browser-based tool to slice sprite sheets and export frames as a ZIP of PNGs.

- Open `index.html` in your browser
- Load a sprite sheet (drag & drop or file picker)
- Create / auto-detect slices
- Export all slices as centered PNG frames in a ZIP

## Features

### Navigation & Precision
- **Real Zoom**: zoom in/out with the mouse wheel (zoom is centered on the cursor)
- **Pan**: hold the **middle mouse button** and drag to move around the canvas
- **Reset View**: quickly return to 100% zoom and no pan
- **Mirror view + export**: flip the sprite sheet horizontally/vertically for inspection, and exports will match the mirror toggles
- **Pixel nudging**: move selected slice(s) by **1 pixel** with the arrow keys

### Slice Editing
- **Resizable slices**: select a slice and drag its **handles** (corners + sides) to resize
- **Smart Snapping**: when drawing a slice, the rectangle automatically trims to the first non-transparent pixels inside the drawn area (removes unwanted empty margins)
- **Auto-trim (single slice)**: instantly trim the selected slice to its non-transparent content

### Visual Validation
- **Background filters**: switch the canvas background between
  - checkerboard (transparency)
  - solid black
  - solid white
- **Image background color**: optionally draw a solid color behind the sprite sheet (display only) using a color picker
- **Onion skinning**: when a slice is selected, the previous slice is drawn at **30% opacity** underneath (aligned by pivot when available)
- **Animation preview**: floating panel to preview a frame sequence in a loop

### Production-Friendly Alignment
- **Pivot points per slice**: set an origin point per frame (useful to prevent “jumping” in-game)
- Preview playback keeps the **pivot fixed** between frames when available

## How to Use

1. Open `index.html` in a modern browser (Chrome/Edge/Firefox).
2. Load an image:
   - Click **Load Image**, or
   - Drag & drop onto the page
3. Choose a mode:
   - **Manual**: draw slices by dragging on the canvas
   - **Auto-Detect**: detect connected non-transparent regions using an alpha threshold
    - Choose **X Order** (Left→Right or Right→Left) to control slice ordering (sorted by X first)
4. Export:
   - Click **Export ZIP** to download `sprites.zip`

Tip: set a **Sheet ID** (in the Project section). It will be used as the ZIP name and the frame filename prefix.

## Controls

### Canvas Navigation
- **Wheel**: zoom
- **Middle mouse drag**: pan

### Selection
- Click a slice to select it
- **Ctrl (or Cmd) + click**: toggle selection
- **Shift + click**: add to selection
- **Esc**: clear selection
- **Ctrl/Cmd + A**: select all slices

### Editing
- Drag **handles** on a selected slice to resize
- **Arrow keys**: move selected slice(s) by 1px
- **Delete / Backspace**: delete selected slice(s)

### Pivot Points
1. Select a slice
2. Enable **Pivot Edit Mode**
3. Click inside the slice to set the pivot

## Animation Preview

- Click **Animation Preview** to show/hide the floating panel
- Click **Use Selection** to use the current selection as the frame sequence (ordered by slice id)
- Click **Play/Pause**
- Adjust **FPS** for playback speed

Tip: set pivots for each frame first—preview playback uses pivots to keep the character aligned.

## Export Details

- Output: `<sheet-id>.zip` with PNG files in `<sheet-id>/`
- Each exported PNG is **centered into a uniform canvas size**:
  - width = maximum slice width
  - height = maximum slice height

This makes exported frames consistent for many animation pipelines.

## Notes

- Auto-detection is based on the alpha channel using your configured **Alpha Threshold**.
- Auto-detect advanced options:
  - **Noise Cleanup (px)**: removes tiny speck noise (helps with background dots)
  - **Bridge Gaps (px)**: connects small pixel gaps (helps thin/fragmented shapes)
  - **Merge Nearby (px)** + **Color Tolerance**: associates nearby fragments with a main body if they’re close and color-similar
  - **Show Oriented Boxes (OBB)**: overlays a rotated fitting box for thin/diagonal shapes
- Smart snapping and auto-trim also use the alpha channel.
- Everything runs locally in your browser—no server needed.

## Tech

- Single-file app: `index.html`
- Dependencies (CDN):
  - `JSZip` for ZIP generation
  - `FileSaver.js` for downloads

## License

If you plan to publish this publicly, consider adding a license file (MIT is a common choice).
