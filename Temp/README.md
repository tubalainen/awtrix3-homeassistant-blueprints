# AWTRIX 3 Indoor Temperature Blueprint

Display the temperature from any indoor temperature sensor on your AWTRIX 3 display using MQTT.

This blueprint allows you to select any temperature sensor in Home Assistant and automatically publishes the current temperature to your AWTRIX device. The temperature is displayed in degrees Celsius (°C) with a dedicated temperature icon.

## Features

- Select any indoor temperature sensor
- Displays temperature in °C
- AWTRIX 3 compatible
- MQTT based
- Easy blueprint import
- Simple setup and configuration

## Requirements

Before using this blueprint:

1. Ensure MQTT is configured and working in Home Assistant.
2. Install and configure your AWTRIX 3 device.
3. Upload icon **6980** to your AWTRIX device.

## Default Icon

This blueprint uses the following AWTRIX icon by default:

| Purpose | Icon ID |
|----------|----------|
| Temperature | 6980 |

> **Important:** Icon **6980** must be uploaded to your AWTRIX device before using this blueprint. Otherwise, the temperature icon will not be displayed correctly.

You are free to replace the icon with another one if desired. Simply upload your preferred icon to the AWTRIX device and update the icon ID in the blueprint.

## Import Blueprint

Click the button below to import the blueprint directly into Home Assistant:

[![Open your Home Assistant instance and import this blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://github.com/tubalainen/awtrix3-homeassistant-blueprints/blob/main/Temp/indoor_temp.yaml)

## Installation

1. Import the blueprint using the button above.
2. Create a new automation from the imported blueprint.
3. Select the indoor temperature sensor you want to display.
4. Configure your AWTRIX MQTT topic if required.
5. Save the automation.

The display will automatically update whenever the selected temperature sensor changes state.

## Example Display

| Sensor Value | Display |
|--------------|----------|
| 21.3°C | 🌡️ 21.3°C |
| 18.7°C | 🌡️ 18.7°C |
| 24.5°C | 🌡️ 24.5°C |

## Contributing

Suggestions, improvements, and pull requests are always welcome. Feel free to help improve these blueprints for the AWTRIX and Home Assistant community.

If you find this blueprint useful, please consider giving the repository a ⭐ on GitHub.
