# awtrix3-homeassistant-blueprints

Home Assistant blueprints & helpers for [AWTRIX 3](https://github.com/Blueforcer/awtrix3)
displays (Ulanzi TC001 / DIY matrix), driven over MQTT.

See each blueprint's own `README.md` for setup instructions.

## Blueprints

| Blueprint | Description |
|-----------|-------------|
| [RSS Feed Headlines](RSS_feed/) | Pushes the latest headlines from any RSS feed to an AWTRIX 3 display as a Custom App. Choose how many headlines to show, whether the icon stays fixed or scrolls away (`pushIcon`), and a custom icon (defaults to LaMetric RSS icon #85). Available as an **all-in-one package** (helpers + REST sensor + automation in one file) **or** a blueprint. |


 Blueprint | Description |
|-----------|-------------|
| [Indoor Temp](Temp/) | Let you choose and display a indoor temp senor on AWTRIX 3 display as a Custom App. with a custom icon (defaults to LaMetric Temp icon #6980). 


 Blueprint | Description |
|-----------|-------------|
| [Weather](weather/) | Let´s you display todays weather and tomorrows using the built in met.no integration and display it on your Awtrix 3 display as custom app

 Blueprint | Description |
|-----------|-------------|
| [Power Usage](power_usage/) | Let´s you display total power usage of your home on the Atrix 3 dispaly as a custom app
