# AWTRIX 3D Printer Status

Display the current status and print progress of your 3D printer on an AWTRIX 3 / Ulanzi display using MQTT.

Unlike most existing AWTRIX automations, this blueprint is **printer agnostic**. Simply select the status and progress sensors from your own Home Assistant installation, making it compatible with virtually any 3D printer integration, including:

- Bambu Lab
- OctoPrint
- Klipper / Moonraker
- PrusaLink
- Creality
- ...and many more

The blueprint automatically displays the print progress while printing, changes to **Done** when the print finishes, and automatically removes itself from the display after a configurable amount of time.

---

## Features

- 🖨️ Works with almost any Home Assistant 3D printer integration
- 📊 Live print progress (0–100%)
- 📈 Built-in progress bar
- 🔄 Automatic printer status detection
- ▶️ Printing, ⏸️ Paused, ❌ Error and ✅ Finished states
- 🧹 Automatically removes itself after a completed print
- 👻 Automatically hides when the printer is idle or offline
- 🏷️ Custom printer name
- 🎨 Custom AWTRIX icon
- 📡 MQTT based
- ✅ AWTRIX 3 compatible
- 🚀 Easy Blueprint import

---

## Requirements

Before using this blueprint you will need:

- Home Assistant
- MQTT configured and working
- An AWTRIX 3 / Ulanzi display
- A Home Assistant integration exposing:
  - Printer Status
  - Print Progress

No specific printer integration is required.

---

## Import Blueprint

[![Open your Home Assistant instance and import this blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://github.com/tubalainen/awtrix3-homeassistant-blueprints/blob/main/3D_Printer/3DPrinter_Status.yaml)

---

## Configuration

After importing the blueprint, create a new automation and configure the following settings.

### AWTRIX Base MQTT Topic

Examples:

```text
awtrix
awtrix_968580
```

The blueprint automatically creates the final MQTT topic:

```text
<Base Topic>/custom/<App Name>
```

Example:

```text
awtrix/custom/printer_status
```

---

### Printer Name

The name displayed on the AWTRIX display.

Examples:

```text
P1S
X1C
Voron
MK4
Printer
```

---

### Printer Status Sensor

Select the entity that reports the current printer state.

Typical values include:

```text
printing
paused
finished
done
idle
offline
error
```

---

### Print Progress Sensor

Select the entity that reports the current print progress.

Expected values:

```text
0
25
50
75
100
```

---

### Remove After Finished

Choose how long the **Done** message remains visible before the app is automatically removed.

Example:

```text
15 minutes
```

---

### Icon

Enter any AWTRIX icon ID.

Example:

```text
15131
```

Make sure the icon has been uploaded to your AWTRIX device.

---

## Display States

### 🖨️ Printing

Displays:

```text
P1S 42%
```

A live progress bar is drawn along the bottom row of the display.

---

### ⏸️ Paused

Displays:

```text
P1S Pause
```

---

### ❌ Error

Displays:

```text
P1S Error
```

---

### ✅ Finished

Displays:

```text
P1S Done
```

After the configured delay, the app is automatically removed from the display.

---

### 👻 Idle / Offline

When the printer is idle, offline or unavailable, the blueprint automatically removes the app from the AWTRIX display.

---

## Automatic Progress Bar

The blueprint draws a live progress bar across the bottom row of the AWTRIX display.

As the print progresses from **0%** to **100%**, the progress bar fills automatically.

---

## Example

During a print:

```text
P1S 67%
```

When finished:

```text
P1S Done
```

After the configured delay:

- The AWTRIX app is automatically removed.

---

## Why another 3D Printer Blueprint?

Most available AWTRIX automations are written specifically for one printer platform.

This blueprint was designed to be **generic**, allowing any Home Assistant user to simply select their own printer sensors without modifying a single line of YAML.

The goal is one blueprint that works with almost every Home Assistant-compatible 3D printer integration. :contentReference[oaicite:0]{index=0}

---

## Future Ideas

Potential future enhancements include:

- ⏳ Remaining print time
- 🧱 Current layer / total layers
- 📄 Filename currently printing
- 🧵 Filament type
- 🌡️ Nozzle and bed temperature
- ⚖️ Filament usage
- ⏱️ Elapsed print time

The blueprint has been designed to make these additions possible without breaking compatibility.

---

## Contributing

Suggestions, improvements, bug reports and pull requests are always welcome.

If your printer integration exposes additional useful sensors, feel free to contribute improvements.

---

## Credits

Created by **MrGlenn-tech**

Inspired by the amazing Home Assistant and AWTRIX communities. :contentReference[oaicite:1]{index=1}

If you find this blueprint useful, please consider giving the repository a ⭐ on GitHub.
