# BevandaBot-kiosk

A lightweight self-service kiosk for tracking consumed inventory (food/beverages) in non-commercial settings (e.g., community centers, clubs, associations). Designed for Raspberry Pi with a 7" HDMI touchscreen.

No fiscal registers, no PC required—just a Raspberry Pi, a screen, and a USB drive for daily reports.

---

## Purpose

This tool allows users to:
- Select items they have taken from a shared stock
- Keep a running count per item
- Export a daily summary (CSV) to a USB drive

All data resets to zero on each program launch—no persistent session history. Only the **product list** is saved between runs.

---

## Requirements

### Hardware
- Raspberry Pi 3B or newer (will work on any python environment and on Rpi 0w and 0 2w)
- HDMI touchscreen (tested on chinese  7" display)
- USB drive (for CSV/excel export)

### Software
- Raspberry Pi OS (with desktop environment)
- Python 3.7+
- `sv-ttk` (Sun Valley ttk theme)

---

## Installation

1. Copy the `kiosk/` folder to a USB drive (e.g., `/media/pi/USB/kiosk`)
2. Run the install script:
   ```bash
   /media/pi/USB/kiosk/install.sh
   ```
3. To start automatically on boot, add this line to `~/.config/lxsession/LXDE-pi/autostart`:
   ```ini
   @/media/pi/USB/kiosk/run_kiosk.sh
   ```
4. (Optional) For portrait mode, add to `/boot/config.txt`:
   ```ini
   display_rotate=1
   ```
5. Reboot.

The app will launch in fullscreen on startup.

---

## File Structure

```
kiosk/
├── main.py             # Main application
├── products.json       # Product list (auto-created if missing)
├── config.json         # UI settings (zoom, items per page)
├── install.sh          # Installs sv-ttk
└── run_kiosk.sh        # Launch script
```

- `products.json` defines available items. Quantities are **not saved** between sessions.
- `config.json` stores user-adjustable UI preferences.

---

## Usage

- Tap **“+”** to increment an item
- Tap **“–”** to decrement (minimum: 0)
- Open the ☰ menu to:
  - Export current counts to CSV (saved to USB as `consumi_YYYYMMDD_HHMMSS.csv`)
  - Add new products
  - Adjust zoom and number of items per page

The CSV includes **all products**, even those with quantity = 0.

---

## Dependencies

- [`sv-ttk`](https://github.com/rdbende/Sun-Valley-ttk-theme) – modern Tkinter theme  
  (installed automatically via `install.sh`)

Built with standard library modules: `tkinter`, `json`, `os`, `datetime`.

---

## License

GNU General Purpose

--- 

This tool is intended for internal inventory tracking in informal, non-commercial environments.
