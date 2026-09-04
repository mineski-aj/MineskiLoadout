# Changelog

## 2026-09-05

### Added
- **Shared team Projects** — save, open, rename, and delete named projects backed by Firebase Firestore, so the whole team works off the same shared library instead of separate per-browser storage. Auto-syncs ~900ms after any edit; falls back to local-only mode with a warning if Firestore isn't reachable.
- **Space-to-pan "grab" tool** — hold Space and drag anywhere on the canvas (even over nodes) to pan, like Figma/Photoshop. Cursor shows an open hand while held.
- **Move nodes from anywhere on the cell**, not just the header strip.
- **Double-click to rename** now works on every node type (previously only worked on Group Box nodes).
- **"📋 Copy List"** button on the Equipment List tab — copies the same report as Export CSV to the clipboard as tab-separated text, so it pastes into Sheets/Excel as individual cells.
- **Per-device "📋 Copy"** button on every I/O List card — copies just that device's I/O block.
- **Floating Undo/Redo panel** pinned to the top-left of the canvas, collapsible via a small handle (remembers collapsed/expanded state).
- **"Extras ▾" dropdown** — Overall Broadcast Inventory, Floorplan, Comms Plotting, and Org Chart collapse into one dropdown whenever the topbar doesn't have room for every tab (e.g. browser zoomed in). Diagram, Equipment List, and I/O List always stay visible.

### Changed
- I/O List's save/export/copy format changed to number-on-each-outer-edge layout (`[in #][input][blank][output][out #]`) with INPUT/OUTPUT headers, matching each device's on-canvas port layout.
- Topbar reorganized: Labels/Curved/Flow/Theme consolidated into one "⚙ Settings" dropdown; Import/Export/Clear consolidated into one "📁 File" dropdown, placed ahead of the Diagram tab. "Clear" renamed to "Clear All" (kept its existing confirmation prompt).
- I/O List tab moved next to Equipment List.
- Removed the redundant "📋 Equip. List" shortcut button (the Equipment List tab already covers it).

### Fixed
- Project names containing special characters (e.g. a colon, as in "CODM: BR") broke every click handler in the Projects list — switched to `data-*` attributes with a delegated click handler instead of embedding names in inline `onclick` JS.
- Clicking the canvas after typing in the sidebar search box left keyboard focus stuck in the search box, so Space-to-pan (and other shortcuts) silently did nothing. Canvas clicks now explicitly return focus to the canvas.
