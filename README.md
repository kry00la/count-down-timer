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

### Set a time
Click **Set Time** to open the time picker. Enter hours, minutes, and seconds, then click **Apply**.

### Start / Pause / Resume / Reset
- **Start** — begins the countdown from the configured time.
- **Pause** — freezes the timer. The button changes to **Resume**.
- **Resume** — continues from where it was paused.
- **Reset** — clears the timer back to zero and unlocks the time picker.

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

## Live (Display) tabs

Display tabs show the timer full-screen with no controls — ideal for projecting on a screen or a second monitor.

### Take Control
If you need to control the timer from a display tab, hover anywhere on the page to reveal the **profile icon button** in the bottom-left. Clicking it promotes that tab to Controller and demotes the previous one.

---

## Automatic failover

If the Controller tab is closed while the timer is running, a Live tab will detect the silence (within ~5 seconds) and automatically promote itself to Controller, keeping the countdown going without interruption.

---

## Persistence

Timer state is saved to `localStorage`, so refreshing a tab or reopening the file will restore the last known state (remaining time, running/paused status).

---

## Browser support

Requires a modern browser that supports the `BroadcastChannel` API:

- Chrome / Edge 54+
- Firefox 38+
- Safari 15.4+

> **Note:** Tabs must be in the **same browser** and loaded from the **same origin** (e.g. all opened as `file://` or all served from the same domain) for syncing to work.
