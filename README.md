# Synced Timer

A fullscreen countdown timer that syncs in real time across multiple browser tabs using the `BroadcastChannel` API and `localStorage`. No server, no install — just open the HTML file.

---

## Quick Start

1. Open `countdown-timer.html` in your browser (double-click the file, or drag it into a browser window).
2. The first tab automatically becomes the **Controller**.
3. Open the same file in more tabs or windows — they become **Live** displays that mirror the controller in real time.

---

## Roles

| Badge | Color | What it means |
|---|---|---|
| **Controller** | Green | This tab controls the timer. All start/pause/reset actions happen here. |
| **Live** | Yellow | This tab is a read-only display. It follows the controller automatically. |
| **Detecting** | Grey | The tab is figuring out its role (lasts ~400 ms on load). |

---

## Controller — what you can do

### Settings panel
Click **Settings** to open the settings panel. From here you can:
- Set the countdown time (hours, minutes, seconds)
- Enter a message to display above the timer
- Choose or remove a background video
- Toggle sound on/off

Click **Apply** to save changes, or **Cancel** to close without saving.

### Start / Pause / Resume / Reset
- **Start** — begins the countdown from the configured time.
- **Pause** — freezes the timer. The button changes to **Resume**.
- **Resume** — continues from where it was paused.
- **Reset** — clears the timer back to zero.

### Keyboard shortcut
Press **Space** to start, pause, or resume the timer at any time — without reaching for the mouse. Spacebar is ignored when a number input is focused or the Settings panel is open.

### Adjust on the fly
The **+** and **−** circle buttons in the bottom-right corner add or subtract **1 minute** at any time — even while the timer is running.

### Color warnings
The digits change color as time runs low:

| Time remaining | Color |
|---|---|
| > 30 seconds | Cream (default) |
| ≤ 30 seconds | Amber |
| ≤ 10 seconds | Red |

A yellow screen flash fires when the countdown hits zero.

---

## Sound

### Tick sounds
A click sound plays on each of the last 10 seconds of the countdown.

### Finish alarm
Three rising beeps play when the timer reaches 00:00.

### Muting
Open **Settings** — the speaker icon button next to Apply/Cancel toggles sound on and off. The icon turns red when muted. This preference is saved to `localStorage` and persists across refreshes.

---

## Message

Open **Settings** and type in the **Message** field to display a line of text above the timer. The message syncs to all Live tabs when you click Apply and persists across refreshes. Clear the field and Apply to remove it.

---

## Background video

Open **Settings** and click **Choose Video** to set a local video file as a full-screen background. A dark overlay is applied automatically so the timer remains readable. The video loops silently.

The selected video is stored in `IndexedDB` and syncs to all Live tabs automatically — any open Live tab will load and play the same video without requiring a separate file pick. The video also persists across page refreshes.

Click the **×** button next to the filename to remove the video from all tabs.

---

## Live (Display) tabs

Display tabs show the timer full-screen with no controls — ideal for projecting on a screen or a second monitor. Tick and finish sounds play on Live tabs too.

### Take Control
If you need to control the timer from a display tab, hover anywhere on the page to reveal the **profile icon button** in the bottom-left. Clicking it promotes that tab to Controller and demotes the previous one.

---

## Automatic failover

If the Controller tab is closed while the timer is running, a Live tab will detect the silence (within ~5 seconds) and automatically promote itself to Controller, keeping the countdown going without interruption.

---

## Persistence

Timer state (including the message) is saved to `localStorage` and background video to `IndexedDB`, so refreshing a tab or reopening the file will restore the last known state (remaining time, running/paused status, message, and background video).

---

## Browser support

Requires a modern browser that supports the `BroadcastChannel` API:

- Chrome / Edge 54+
- Firefox 38+
- Safari 15.4+

> **Note:** Tabs must be in the **same browser** and loaded from the **same origin** (e.g. all opened as `file://` or all served from the same domain) for syncing to work.
