# AWTRIX 3 Power Usage Blueprint

Display your home's current power consumption on an AWTRIX 3 display using MQTT.

This blueprint allows you to select any Home Assistant power sensor and automatically formats the value for display on your AWTRIX device. Power consumption is color-coded for quick visual feedback and supports sensors reporting in both watts (W) and kilowatts (kW).

## Features

- Select any power sensor in Home Assistant
- Automatic W/kW conversion
- Dynamic color coding based on power consumption
- AWTRIX 3 compatible
- MQTT based
- Easy blueprint import

## Requirements

Before using this blueprint:

1. Install and configure the AWTRIX 3 integration.
2. Ensure MQTT is configured and working in Home Assistant.
3. Upload icon **50785** to your AWTRIX device, as this blueprint uses that icon for the power display.

## Installation

Click the button below to import the blueprint directly into Home Assistant:

[![Open your Home Assistant instance and import this blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://github.com/tubalainen/awtrix3-homeassistant-blueprints/blob/main/power_usage/Power_usage.yaml)

## Configuration

After importing:

1. Create a new automation from the blueprint.
2. Select the power sensor you want to display.
3. Configure your AWTRIX MQTT topic if needed.
4. Save the automation.

The display will automatically update whenever the selected power sensor changes state.

## Example

| Power Usage | Display |
|------------|---------|
| 850 W | Green |
| 2.4 kW | Yellow |
| 4.8 kW | Orange |
| 7.2 kW | Red |

## Contributing

Feel free to submit issues, suggestions, or pull requests to improve the blueprint for the Home Assistant and AWTRIX community.
