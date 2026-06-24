# AWTRIX 3 Nordpool Electricity Price Blueprint

Display the current Nordpool electricity price and a 24-hour price overview on your AWTRIX 3 / Ulanzi display using MQTT.

This blueprint retrieves electricity prices from a Nordpool sensor in Home Assistant and displays the current price together with a visual 24-hour price bar graph directly on your AWTRIX display.

The current price is color-coded based on configurable price thresholds, making it easy to see at a glance whether electricity is currently cheap, moderate, or expensive.

## Features

- Display current Nordpool electricity price
- 24-hour visual price graph
- Configurable color thresholds
- Supports any Nordpool sensor
- Configurable unit and multiplier
- AWTRIX 3 compatible
- MQTT based
- Easy blueprint import

## Requirements

Before using this blueprint:

1. Home Assistant installed and running.
2. MQTT configured and working.
3. An AWTRIX 3 / Ulanzi display connected via MQTT.
4. The Nordpool integration installed and configured.
5. A Nordpool sensor that provides hourly electricity prices.
6. Icon **54077** uploaded to your AWTRIX device.

## Default Icon

This blueprint uses the following AWTRIX icon by default:

| Purpose | Icon ID |
|----------|----------|
| Electricity Price | 54077 |

> **Important:** Icon **54077** must be uploaded to your AWTRIX device before using this blueprint. Otherwise, the electricity price icon will not be displayed correctly.

## Import Blueprint

[![Open your Home Assistant instance and import this blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://github.com/tubalainen/awtrix3-homeassistant-blueprints/blob/main/Electric_Price/electric_price_now.yaml)

## Configuration

After importing the blueprint, create a new automation and configure the following settings:

### Nordpool Sensor

Select the Nordpool sensor that provides your electricity prices.

Example:

```text
sensor.nordpool_kwh_se3_sek_3_10_025
```

### Hourly Attribute

Normally:

```text
today
```

This attribute contains the hourly price values used to generate the 24-hour graph.

### Display Unit

Examples:

```text
kr
SEK/kWh
öre
c/kWh
```

For the shortest display without scrolling, `kr` is recommended.

### Price Multiplier

Use:

| Sensor Value | Multiplier |
|-------------|------------|
| Already in SEK/kWh | 1 |
| EUR/kWh → display cents | 100 |
| SEK/kWh → display öre | 100 |

### Color Thresholds

Example configuration for Swedish electricity prices:

| Price Range | Color |
|------------|--------|
| Below 1 kr/kWh | Green |
| 1–2 kr/kWh | Yellow |
| Above 2 kr/kWh | Red |

Suggested values:

```text
Low Price Limit: 1
Medium Price Limit: 2
```

## Example Display

Current price:

```text
1.13 kr
```

Price color:

- 🟢 Green = Cheap
- 🟡 Yellow = Moderate
- 🔴 Red = Expensive

The bottom row of the AWTRIX display shows a 24-hour visual price overview where each pixel represents one hour of the day.

## Troubleshooting

### Price does not appear

Verify that:

- MQTT is connected and working.
- The AWTRIX MQTT topic is correct.
- The Nordpool sensor is available.
- The selected hourly attribute exists.
- Icon 54077 has been uploaded to AWTRIX.

### Incorrect price shown

Check:

- Display Unit
- Price Multiplier

Most Nordpool sensors reporting SEK/kWh should use:

```text
Display Unit: kr
Price Multiplier: 1
```

### Display Scrolls

To minimize scrolling, use a shorter display unit:

```text
kr
```

instead of:

```text
SEK/kWh
```

## Contributing

Suggestions, improvements, bug reports, and pull requests are always welcome.

Feel free to help improve these blueprints for the AWTRIX and Home Assistant community.

If you find this blueprint useful, please consider giving the repository a ⭐ on GitHub.
