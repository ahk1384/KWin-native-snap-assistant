# KWin Native Snap Assistant (v2.0)

A modern, dynamic **Windows 11-style Snap Assist** for KDE Plasma 6.

When you snap a window (via mouse drag, corner snap, or keyboard shortcut), Snap Assist immediately presents open windows as interactive thumbnail cards in the unoccupied screen area, allowing you to rapidly complete your desktop layout.

---

## ✨ Features

- **Dynamic Zone Detection (All Layouts Supported)**:
  - **Halves**: Left/Right 50% vertical split, Top/Bottom 50% horizontal split (ideal for portrait monitors).
  - **Quarters (4 Quadrants)**: Top-Left, Top-Right, Bottom-Left, Bottom-Right corner snapping.
  - **Thirds & Ultrawide**: Left 1/3, Center 1/3, Right 1/3, and 25/50/25 center-focus layouts.
  - **Asymmetric Splits**: 70/30 or 2/3 + 1/3 configurations.
  - **KWin Native Custom Zones**: Integrates with custom layouts configured in Plasma 6 (`Meta + T`).
- **Sequential Multi-Zone Chaining**:
  - Snapping into a 3-zone or 4-zone layout prompts you in each empty zone sequentially until the entire screen layout is filled.
- **Windows 11 Fluent Acrylic UI**:
  - Frosted glass/acrylic panel positioned directly within the target empty zone.
  - Live window thumbnails (`WindowThumbnail`) preserving aspect ratio.
  - Native application icons (`Kirigami.Icon`) and truncated title captions.
  - Smooth entrance animations and fluid sliding transitions between chained zones.
  - System accent color highlight borders and subtle hover scale elevation.
- **Fast Keyboard & Mouse Navigation**:
  - **Number Badges (1–9)**: Press any number key to immediately select and snap that candidate.
  - **Arrow Keys**: Navigate the grid with Up/Down/Left/Right, confirm with Enter or Space.
  - **Close Button (✕)**: Hovering over any card reveals a close button to dismiss unwanted windows directly from the assistant.
  - **Escape / Click Outside**: Press Escape or click outside the panel to dismiss without tiling.
- **Multi-Monitor Awareness**:
  - Accurately identifies monitor outputs, client work areas, and prevents cross-screen leakage.
- **Smart Candidate Filtering**:
  - Filters out windows that are already tiled in other zones.
  - Respects virtual desktops and current screen outputs.
  - Suppresses itself when all screen zones are already filled.

---

## 🚀 Installation

Run these commands from the directory containing the repository:

```bash
kpackagetool6 --type=KWin/Script --install .
```

Or from the parent directory:

```bash
kpackagetool6 --type=KWin/Script --install KWin-native-snap-assistant
```

Enable **Snap Assist** in **System Settings → Window Management → KWin Scripts**.

### Upgrade an existing installation

```bash
kpackagetool6 --type=KWin/Script --upgrade .
```

### Remove

```bash
kpackagetool6 --type=KWin/Script --remove snap-assist
```

---

## ⚙️ Configuration

Settings can be customized in `contents/config/config.json`:

```json
{
    "skipPickerOnKeyboardSnap": false,
    "closePickerOnClickOutside": true,
    "suppressPickerWhenAllFilled": true,
    "enableMultiZoneChaining": true,
    "autoSelectSingleCandidate": false,
    "showNumberShortcuts": true,
    "showWindowIcons": true,
    "showCloseButtonOnHover": true,
    "animationSpeedMs": 220
}
```

| Option | Default | Description |
|---|---|---|
| `skipPickerOnKeyboardSnap` | `false` | When `false`, snapping via keyboard (`Meta + Left/Right/Up/Down`) invokes Snap Assist just like mouse snapping. Set to `true` for silent keyboard tiling. |
| `closePickerOnClickOutside` | `true` | Clicking anywhere outside candidate cards (desktop, panel, snapped window) dismisses assist. |
| `suppressPickerWhenAllFilled` | `true` | When all layout zones on the screen are occupied by tiled windows, Snap Assist suppresses itself. |
| `enableMultiZoneChaining` | `true` | When multiple zones are empty (e.g. 4 quarters), sequentially prompts for each empty zone. |
| `autoSelectSingleCandidate` | `false` | When only 1 candidate window is available, automatically snaps it without waiting for input. |
| `showNumberShortcuts` | `true` | Overlays `1`, `2`, `3` badges on cards for fast number-key selection. |
| `showWindowIcons` | `true` | Displays application icons in candidate cards. |
| `showCloseButtonOnHover` | `true` | Displays a close button on card hover to close unwanted windows. |
| `animationSpeedMs` | `220` | Duration of entrance and zone-transition animations in milliseconds. |

---

## 🛠️ Development & Reloading

To reload the script via D-Bus after modifying code:

```bash
qdbus6 org.kde.KWin /Scripting unloadScript snap-assist
qdbus6 org.kde.KWin /Scripting start
```

### Live Logs

To inspect Snap Assist events:

```bash
journalctl --user -f QT_CATEGORY=qml QT_CATEGORY=kwin_scripting | grep --line-buffered 'snap-assist:'
```

### Code Validation

```bash
qmllint contents/ui/main.qml
git diff --check
```

---

## 📜 License

GPL-3.0-or-later.
