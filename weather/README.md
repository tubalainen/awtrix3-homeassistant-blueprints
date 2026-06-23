# AWTRIX 3 Weather Blueprints

Display today's and tomorrow's weather forecast on your AWTRIX 3 display using Home Assistant's built-in Met.no weather integration.

These blueprints retrieve weather data directly from Home Assistant and present it in a compact, easy-to-read format on your AWTRIX display.

To minimize scrolling on the display, the default labels are abbreviated:

- **NU** = Current weather ("Nu" in Swedish)
- **IM** = Tomorrow ("Imorgon" in Swedish)

You can customize these labels in the blueprint if preferred. Keep in mind that labels longer than three characters may cause the text to scroll on the AWTRIX display.

## Features

- Current weather display
- Tomorrow's weather forecast
- Uses Home Assistant's built-in Met.no Weather integration
- AWTRIX 3 compatible
- MQTT based
- Compact display format to reduce scrolling
- Easy blueprint import

## Requirements

Before using these blueprints:

1. Install and configure the **Met.no Weather** integration in Home Assistant.
2. Ensure MQTT is configured and working.
3. Install the default weather icons listed below on your AWTRIX device.

## Default Icons Used By The Blueprints

These blueprints use the following AWTRIX icon IDs by default:

| Icon ID |
|----------|
| 11201 |
| 12181 |
| 22160 |
| 2283 |
| 2284 |
| 2289 |
| 49301 |
| 55032 |
| 60936 |
| 73790 |
| 73809 |

> **Important:** These icons must be uploaded to your AWTRIX device before using the blueprints. If an icon is missing, the corresponding weather condition may not display correctly.

You are free to replace these icons with your own. Simply upload the new icons to your AWTRIX device and update the icon IDs in the blueprint.

## Blueprints

### Current Weather

Displays the current weather conditions.

[![Open your Home Assistant instance and import this blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://github.com/tubalainen/awtrix3-homeassistant-blueprints/blob/main/weather/weather_today.yaml)

### Tomorrow's Forecast

Displays tomorrow's weather forecast.

[![Open your Home Assistant instance and import this blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://github.com/tubalainen/awtrix3-homeassistant-blueprints/blob/main/weather/weather_tomorrow.yaml)

## Installation

1. Import one or both blueprints using the buttons above.
2. Create a new automation from the imported blueprint(s).
3. Select your weather entity from the Met.no integration.
4. Configure your AWTRIX MQTT topic if required.
5. Save the automation.

The display will automatically update with the latest weather information.

## Example Display

| Label | Description |
|---------|-------------|
| NU | Current weather conditions |
| IM | Tomorrow's weather forecast |

## Contributing

Suggestions, improvements, and pull requests are always welcome. Feel free to help improve these blueprints for the AWTRIX and Home Assistant community.

If you find this blueprint useful, please consider giving the repository a ⭐ on GitHub.
