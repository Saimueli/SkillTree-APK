# SkillTree 3.0

A minimalist, dark-mode skill tree tracker for Android (WebView-based PWA). Build, visualize and track your personal growth — from "Life" at the root down to individual goals and tasks.

---

## ✨ Features

### 🌳 Tree visualization
- Interactive SVG canvas with infinite pan & zoom
- **Start node** (⭐ `Life`) — your root, styled in gold
- **Category / Branch nodes** (🔷) — grouped topics, outlined in **blue**
- **Task nodes** (🟩) — actionable items with three statuses:
  - ⚪ **In Progress** → **gray** outline
  - 🟢 **Done** → **green** outline
  - 🔴 **Not Done** → **red** outline
- Curved Bézier links connecting parents to children — link color always matches the destination node's type
- Auto-layout (tidy top-down tree) + manual drag positioning

### 🎯 Focus Goal
- Mark **one** task as your current focus
- It gets a golden glow on the canvas + a pill in the top-left corner
- Tap the pill to jump straight to it
- Only one focus goal can exist at a time

### 1️⃣ Goal Steps
- Assign numbered steps to tasks (1, 2, 3…)
- Useful for ordering milestones or a roadmap
- Step numbers auto-renumber when removed
- Badge in the top-right of each node shows `★` (focus) or step number

### 👆 Gestures

| Gesture | Action |
|---|---|
| **Tap** node | Select it (opens the bottom action bar) |
| **Tap** empty space | Deselect / start pan |
| **Drag** node | Move it freely |
| **Drag** empty space | Pan the canvas |
| **Pinch** | Zoom (30 % – 160 %) |
| **Scroll wheel** | Zoom at cursor |
| **Long-press** node (> 500 ms) → release | Open node context menu |
| **Long-press** then **drag** | Cancels the menu, keeps dragging |
| **Right-click** node | Same context menu (desktop) |

Long-press feedback: the node pulses in its **own type color** (gold / blue / gray / green / red) so you know exactly what you're aiming at.

### 🖱️ Context Menu
- 🎯 **Set / Clear Focus Goal**
- 1️⃣ **Add / Remove Goal Step**
- ✎ **Edit** (title, type, status, description)
- 🗑 **Delete** (with entire subtree)

### ↶ Undo
- Ctrl + Z / Cmd + Z
- Undo history of 10 actions
- Currently supports **Delete** and **Reset**

### 📋 Import / Export
- **Copy JSON** — dumps the full tree state to clipboard
- **Paste JSON** — restores a tree from JSON (validates structure, de-duplicates focus & steps)
- Everything is stored in `localStorage` under `skilltree.v9` (falls back to `skilltree.v8`)

### 🎨 Auto Layout
- Tidy hierarchical layout with configurable horizontal and vertical gaps
- Recenters automatically after Reset
- Manual positions are preserved between sessions until you re-run Auto Layout

---

## 🎨 Color Palette

| Element | Color |
|---|---|
| Background | `#121212` |
| Panel | `#1e1e1e` |
| Text | `#e0e0e0` |
| Start node | `#f59e0b` (gold) |
| Category | `#3b82f6` (blue) |
| Task – In Progress | `#64748b` (gray) |
| Task – Done | `#10b981` (green) |
| Task – Not Done | `#ef4444` (red) |
| Focus glow | `#f59e0b` (gold) |

---

## 📱 Platform

- Single-file `index.html` running inside an Android **WebView**
- Optimized for mobile: safe-area insets (notches), touch-friendly hit areas, `touch-action: none` on the canvas, no accidental overscroll
- Fully offline — no network calls, no external dependencies

---

## 🗂️ Project Structure

    SkillTree/
    ├── app/
    │   └── src/
    │       └── main/
    │           └── assets/
    │               └── index.html      ← the entire app
    └── build/                          ← generated build artifacts

All logic, styling and markup live in **`app/src/main/assets/index.html`**. Edit that file only — the copies under `app/build/` are regenerated on build.

---

## 🚀 Build & Run

1. Open the project in **Android Studio**.
2. Ensure `app/src/main/assets/index.html` is up to date.
3. **Build → Clean Project → Rebuild**.
4. Install `app-debug.apk` on your device or run from Android Studio.

---

## 💾 Data Model

State is stored as a single JSON blob:

    {
      "nodes": [
        {
          "id": "abc123",
          "type": "start",
          "title": "Life",
          "description": "",
          "parentId": null,
          "x": 2000,
          "y": 300
        },
        {
          "id": "def456",
          "type": "branch",
          "title": "Career",
          "description": "",
          "parentId": "abc123",
          "x": 2000,
          "y": 520
        },
        {
          "id": "ghi789",
          "type": "task",
          "title": "Master Kotlin",
          "description": "Finish the advanced course",
          "parentId": "def456",
          "status": "in_progress",
          "focusGoal": true,
          "goalStep": 1,
          "x": 2000,
          "y": 700
        }
      ],
      "view": { "x": 2000, "y": 600, "zoom": 1 }
    }

- `type: "start"` is the root and cannot be deleted
- `type` is one of `"start"`, `"branch"`, `"task"`
- `status` (`in_progress` | `done` | `todo`) applies only to tasks
- `focusGoal: true` on at most one task
- `goalStep` is a unique positive integer; renumbered automatically
- `view` remembers the last camera position

---

## 🧭 Tips

- Start by tapping the **⭐ Life** node → **+ Child** → add your first category
- Give every branch a clear name ("Career", "Health", "Skills") before nesting tasks inside
- Set a **focus goal** to keep one task highlighted while you explore the rest
- Use **Auto Layout** whenever you've been dragging nodes around and want a tidy view
- Back up your tree with **Copy JSON** and paste it into a note — it's your portable snapshot

---

## 📝 Changelog

### 3.0
- 🎨 Swapped link colors: **in-progress** links are gray, **category** links stay blue
- 🔵 Node outlines: in-progress tasks now use **gray**, categories remain blue
- ✨ **Long-press pulse now matches node type color** (gold / blue / gray / green / red) for instant feedback
- 🖱️ Improved long-press interaction: menu opens **on release**, not mid-hold — dragging is never interrupted
- 🎯 Long-press visual feedback prevents accidental menu opening
- 📖 Added this README
- 📄 Licensed under MIT

### 2.x
- Undo system (delete + reset)
- Import / Export JSON
- Auto Layout
- Focus Goal & Goal Steps

### 1.x
- Initial release: SVG tree, node editing, pan/zoom, local persistence

---

## 📄 License

MIT License

Copyright (c) 2025 SkillTree

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
