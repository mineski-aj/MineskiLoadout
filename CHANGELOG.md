# Changelog

## 2026-09-07

### Fixed
- **Floorplan never saved anywhere** — no localStorage, no cloud sync. It only ever lived in the browser tab's memory and vanished on refresh/close, which is why floorplan work wasn't showing up for teammates (and why it could be lost entirely). Now wired into the same save/sync pipeline as every other tab — verified end-to-end against real Firestore, including a fresh-session reopen. Floorplan images are auto-downscaled (max 1800px, re-compressed as JPEG) before syncing so a full-resolution photo doesn't blow the 1 MiB/document Firestore cap for the whole project.

### Added
- **Floorplan tabs** — multiple floorplans per project, each with its own image, scale, and cable runs, switchable like any other tab set in the app (rename via double-click, delete, add). Anyone with existing single-floorplan data gets it migrated automatically into a first tab.
- **Metric/Imperial units toggle** on the Floorplan measurer — a per-viewer display preference (not synced project data, like theme), so each teammate can view the same shared measurements in meters or feet.
- Floorplan drawing tool: **Enter** finishes the run you're currently drawing; **Ctrl+Z** removes just the last-placed waypoint so a misplaced click doesn't force restarting the whole run; a finished run can be **selected** (click its line or its sidebar card) and then have any of its **individual waypoints dragged** to a new position.

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
- **🎯 Center view** button on the floating canvas panel — recenters your viewport on the diagram's actual content, so a scroll/pan that drifts off into empty canvas space no longer looks like lost work.
- **"Collapse All"** button in the equipment sidebar (next to Search) — collapses every category at once, and flips to "Expand All" once everything's collapsed.
- **Vendor / third-party marking** for devices and cables — a "🏷️ Vendor" checkbox in Edit Device / Edit Cable flags an item as not ours. Vendor items are excluded from the Equipment List's counts and its CSV/Copy exports, and get a visual cue on the canvas: a dashed border + corner badge for nodes, a dashed line + label prefix for cables.

### Changed
- Paste (Ctrl+V) now drops the copy centered on your current cursor position on the canvas, instead of always offsetting from the original node's spot.
- Edit Device's Inputs/Outputs fields now cap at 40 (previously 32).
- I/O List's save/export/copy format changed to number-on-each-outer-edge layout (`[in #][input][blank][output][out #]`) with INPUT/OUTPUT headers, matching each device's on-canvas port layout.
- Topbar reorganized: Labels/Curved/Flow/Theme consolidated into one "⚙ Settings" dropdown; Import/Export/Clear consolidated into one "📁 File" dropdown, placed ahead of the Diagram tab. "Clear" renamed to "Clear All" (kept its existing confirmation prompt).
- I/O List tab moved next to Equipment List.
- Removed the redundant "📋 Equip. List" shortcut button (the Equipment List tab already covers it).

### Fixed
- Project names containing special characters (e.g. a colon, as in "CODM: BR") broke every click handler in the Projects list — switched to `data-*` attributes with a delegated click handler instead of embedding names in inline `onclick` JS.
- Clicking the canvas after typing in the sidebar search box left keyboard focus stuck in the search box, so Space-to-pan (and other shortcuts) silently did nothing. Canvas clicks now explicitly return focus to the canvas.
