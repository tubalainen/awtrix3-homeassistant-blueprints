# AWTRIX 3 Countdown Blueprint

Display a customizable countdown timer on your AWTRIX 3 / Ulanzi display using MQTT.

Perfect for counting down to vacations, birthdays, holidays, project deadlines, events, anniversaries, or any other important date.

Each countdown is published as its own AWTRIX Custom App, allowing you to create multiple independent countdowns from the same blueprint.

When the countdown reaches zero, the app is automatically removed from the AWTRIX display.

## Features

- Create unlimited countdowns
- Each countdown uses its own MQTT topic
- Custom display name
- Custom AWTRIX icon
- Custom text color
- Multiple display formats
- Automatically removes itself when finished
- AWTRIX 3 compatible
- MQTT based
- Easy blueprint import

## Requirements

Before using this blueprint:

1. Home Assistant installed and running.
2. MQTT configured and working.
3. An AWTRIX 3 / Ulanzi display connected via MQTT.
4. Any AWTRIX icon you wish to use uploaded to your device.

## Import Blueprint

[![Open your Home Assistant instance and import this blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://github.com/tubalainen/awtrix3-homeassistant-blueprints/blob/main/Countdown/countdown.yaml)

## Configuration

After importing the blueprint, create a new automation and configure the following settings:

### AWTRIX Base MQTT Topic

Examples:

```text
awtrix
awtrix_968580
```

The blueprint automatically creates the final topic:

```text
<Base Topic>/custom/<App Name>
```

Example:

```text
awtrix/custom/countdown_vacation
```

### Countdown App Name

Each countdown should have a unique app name.

Examples:

```text
countdown_vacation
countdown_xmas
countdown_birthday
countdown_wedding
```

This allows multiple countdowns to coexist on the same AWTRIX display.

### Display Name

The text shown on the display.

Examples:

```text
Vacation
Xmas
Birthday
Wedding
```

### Target Date and Time

Select the date and time to count down to.

The countdown updates automatically every minute.

### Icon

Enter any AWTRIX icon ID.

Examples:

```text
56631
6980
54077
```

Make sure the icon has been uploaded to your AWTRIX device.

### Text Color

Any valid HEX color can be used.

Examples:

```text
#00BFFF
#00FF00
#FFFF00
#FF0000
```

### Display Mode

Choose how the remaining time is displayed.

#### Days

Example:

```text
Vacation 14D
```

#### Days Hours

Example:

```text
Vacation 14D 6H
```

#### Days Hours Minutes

Example:

```text
Vacation 14D 6H 32M
```

## Example Use Cases

### Summer Vacation

```text
Display Name: Vacation
Target Date: 2026-07-01
Icon: 56631
```

### Christmas

```text
Display Name: Xmas
Target Date: 2026-12-24
Icon: 49301
```

### Birthday

```text
Display Name: Birthday
Target Date: 2026-09-14
Icon: 6980
```

## Automatic Cleanup

When the countdown reaches zero:

- The countdown app is automatically removed.
- No manual cleanup is required.
- The AWTRIX display will stop showing the countdown.

## Multiple Countdowns

You can create multiple countdowns from the same blueprint.

Examples:

```text
Vacation
Christmas
Birthday
Wedding
New Year
```

Each countdown will appear as its own AWTRIX Custom App.

## Troubleshooting

### Countdown does not appear

Verify:

- MQTT is connected and working.
- The AWTRIX base topic is correct.
- The icon exists on your AWTRIX device.
- The target date is in the future.

### Countdown disappeared

This is expected behavior when the countdown reaches zero.

The blueprint automatically removes the app from AWTRIX once the target date and time has passed.

## Contributing

Suggestions, improvements, bug reports, and pull requests are always welcome.

Feel free to help improve these blueprints for the AWTRIX and Home Assistant community.

If you find this blueprint useful, please consider giving the repository a ⭐ on GitHub.
