# AWTRIX 3 – RSS Feed Headlines (Home Assistant Blueprint)

Shows the latest headlines from any RSS feed on an **AWTRIX 3** display
(Ulanzi TC001 or DIY matrix) as a Custom App, sent over MQTT from Home
Assistant.

| File | Purpose |
|------|---------|
| `rss_feed_awtrix3.yaml` | The Home Assistant **automation blueprint** (import this). |
| `rss_rest_sensor_example.yaml` | One-time REST sensor config – **this is where you set the feed URL.** |
| `README.md` | This guide. |

---

## Features

- **Pick any RSS feed** – the URL is set once in a REST sensor (no HACS required).
- **Pick the AWTRIX device** – by its MQTT topic prefix.
- **Choose how many headlines** show before the app advances (1–20).
- **Icon behaviour** – keep the icon **fixed on the left**, or let the text
  **scroll over / push the icon away** (AWTRIX `pushIcon` 0 / 1 / 2).
- **Custom icon** – any AWTRIX icon ID, filename, or Base64. Defaults to the
  orange LaMetric **RSS icon #85** when left blank.
- **Resilient** – re-pushes on feed updates, on HA start, and on a safety
  interval so it survives an AWTRIX reboot.

---

## Requirements

- Home Assistant with the **MQTT** integration configured and talking to AWTRIX.
- An AWTRIX 3 device subscribed to that MQTT broker.

---

## Setup

### 1. Create the feed sensor (sets the RSS URL)

Open `rss_rest_sensor_example.yaml`, copy the **Standard RSS 2.0** block into
your `configuration.yaml` (or a file under `/config/packages/`), then:

- set `resource:` to your RSS feed URL,
- give the sensor a unique `name` and `unique_id`.

Restart Home Assistant (or *Developer Tools → YAML → Reload REST entities*).
In **Developer Tools → States**, confirm the new `sensor.…` has an **`item`**
attribute containing the feed entries.

> Home Assistant's REST integration auto-converts the feed's XML into a dict,
> so `value_json.rss.channel.item` is the list of items. Atom feeds (`<entry>`)
> have a variant block in the same file.

### 2. Add the icon to the display

On the **AWTRIX web UI → Icons** tab, enter icon ID **`85`** and download it so
it lives on the device's flash. (AWTRIX serves icons from flash; sending an ID
that isn't present shows a blank icon.) Skip this if you'll supply your own
icon ID/Base64 — just download whichever ID you use.

### 3. Import the blueprint

- **Settings → Automations & Scenes → Blueprints → Import Blueprint**, or
- copy `rss_feed_awtrix3.yaml` into `/config/blueprints/automation/<you>/`.

### 4. Create the automation

| Field | What to enter |
|-------|----------------|
| **AWTRIX MQTT topic prefix** | The prefix before `/custom/` (AWTRIX UI → *Network*). Default builds use `awtrix`. No trailing slash. |
| **RSS feed sensor** | The sensor from step 1. |
| **Number of headlines** | 1–20. |
| **Icon behaviour** | Fixed left / scroll-away (no reappear) / scroll-away (reappear). |
| **Icon** | Blank = RSS icon #85, or your own ID / filename / Base64. |
| **Text colour** | Hex, e.g. `#FFA500`. |
| **Headline separator** | Text shown between headlines, e.g. `   •   `. |
| **Safety re-push interval** | Minutes between safety re-sends. |

Save. The app named **`rss`** appears in the AWTRIX rotation.

---

## How it works

The automation builds an AWTRIX
[Custom App](https://blueforcer.github.io/awtrix3/#/api?id=custom-apps-and-notifications)
payload and publishes it to:

```
<prefix>/custom/rss
```

Example payload:

```json
{
  "text": "Headline one   •   Headline two   •   Headline three",
  "icon": "85",
  "pushIcon": 0,
  "color": "#FFFFFF",
  "repeat": 1,
  "scrollSpeed": 100
}
```

- `pushIcon` maps the **icon behaviour** choice:
  `0` icon fixed · `1` scrolls away, no reappear · `2` scrolls away, reappears each loop.
- `repeat: 1` scrolls the full set of headlines once, then the app advances to
  the next app in the AWTRIX loop — i.e. "show N headlines, then move on".

### Removing the app

To delete it from the display, publish an **empty** payload to
`<prefix>/custom/rss` (e.g. via *Developer Tools → Actions → mqtt.publish*).

---

## Notes & limitations

- The RSS **URL lives in the REST sensor**, not the blueprint, because Home
  Assistant automations can't fetch/parse a raw URL on their own. One sensor
  per feed; create several automations to drive several feeds/apps (give each
  a different sensor — and change the app name in the blueprint's `variables`
  if you want them as separate AWTRIX apps).
- Icons are **not** auto-downloaded by ID at send time; add them via the AWTRIX
  web UI first (step 2).
- Titles are passed through `striptags` + trim to drop stray HTML.
