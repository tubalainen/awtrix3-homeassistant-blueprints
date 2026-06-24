# AWTRIX 3 Home Assistant Blueprints

A collection of Home Assistant blueprints and helpers for **AWTRIX 3** displays (Ulanzi TC001 and DIY LED matrix projects) using MQTT.

These blueprints make it easy to display useful information from Home Assistant directly on your AWTRIX device, including weather forecasts, indoor temperature, electricity prices, power consumption, RSS feeds, and more.

## Features

- Easy Home Assistant Blueprint imports
- AWTRIX 3 compatible
- MQTT based
- Configurable sensors and entities
- Community-friendly and customizable
- Supports both Ulanzi TC001 and DIY AWTRIX displays

## Available Blueprints

| Blueprint | Description |
|-----------|-------------|
| 🌐 [RSS Feed Headlines](RSS_feed/) | Display headlines from any RSS feed as a scrolling AWTRIX Custom App. Supports custom icons, configurable headline count, and icon behavior. |
| 🌡️ [Indoor Temperature](Temp/) | Display the temperature from any Home Assistant temperature sensor on your AWTRIX display. |
| ☀️ [Weather Forecast](weather/) | Display current weather conditions and tomorrow's forecast using Home Assistant's built-in Met.no integration. |
| ⚡ [Power Usage](power_usage/) | Display your home's current power consumption with automatic W/kW conversion and color-coded indicators. |
| 💰 [Electricity Price](Electric_Price/) | Display current Nordpool electricity prices together with a 24-hour visual price overview and color-coded pricing levels. |

## Requirements

Most blueprints require:

- Home Assistant
- MQTT configured and working
- An AWTRIX 3 device
- Required icons uploaded to AWTRIX (see each blueprint's README)

Some blueprints may require additional integrations such as:

- Met.no Weather
- Nordpool

Please refer to each blueprint's individual README for detailed setup instructions and requirements.

## Installation

1. Open the blueprint folder you want to use.
2. Open the corresponding README.
3. Click the **Import Blueprint** button.
4. Create a new automation from the imported blueprint.
5. Configure your sensors and AWTRIX MQTT topic.
6. Save and enjoy.

## Supported Hardware

- Ulanzi TC001
- AWTRIX Light
- DIY AWTRIX 3 compatible LED matrix displays

## Contributing

Suggestions, improvements, bug reports, and pull requests are always welcome.

Feel free to contribute new blueprints, improve existing ones, or help expand support for additional Home Assistant integrations.

## Credits

- [Blueforcer / AWTRIX 3](https://github.com/Blueforcer/awtrix3)
- Home Assistant Community
- Contributors to these blueprints

---

If you find this repository useful, please consider giving it a ⭐ on GitHub.
