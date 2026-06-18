# AWTRIX 3 – RSS Feed Headlines (Home Assistant)

Shows the latest headlines from any RSS feed on an **AWTRIX 3** display
(Ulanzi TC001 or DIY matrix) as a Custom App, sent over MQTT from Home
Assistant.

## Two ways to install

| | All-in-one **Package** ⭐ | **Blueprint** + REST sensor |
|---|---|---|
| File(s) | `awtrix3_rss_feed_package.yaml` | `rss_feed_awtrix3.yaml` + `rss_rest_sensor_example.yaml` |
| Feed sensor included? | **Yes** – bundled in the same file | No – you add the REST sensor separately |
| Config | Live UI helpers (URL, count, icon, …) | Blueprint inputs in the automation editor |
| Best for | One self-contained drop-in, change everything from the UI | People who prefer the blueprint import workflow |

> **Why isn't the REST sensor inside the blueprint?**
> A Home Assistant **blueprint targets exactly one domain** (automation *or*
> script *or* template) — by design it cannot also contain a `rest:` sensor.
> A **package**, on the other hand, can bundle every domain (`input_*`, `rest`,
> `automation`) in a single file. That's why the all-in-one option is a package,
> and the blueprint option needs the sensor added alongside it.

---

## Option A — Package (recommended, fully self-contained)

1. Enable packages in `configuration.yaml`:
   ```yaml
   homeassistant:
     packages: !include_dir_named packages
   ```
2. Save [`awtrix3_rss_feed_package.yaml`](awtrix3_rss_feed_package.yaml) as
   `/config/packages/awtrix3_rss_feed.yaml`.
3. Restart Home Assistant.
4. On the **AWTRIX web UI → Icons** tab, download icon ID **85** (or your own).
5. Configure from the created UI helpers (Settings → Devices & Services →
   Helpers): Feed URL, MQTT topic prefix, Number of headlines, Icon behaviour,
   Icon, Text colour, Separator.

The feed URL is read live via the REST sensor's `resource_template`, so changing
the **Feed URL** helper re-fetches immediately. The app is published to
`<prefix>/custom/rss`.

> Helpers use `initial:` values, so they reset to defaults on restart. Delete a
> helper's `initial:` line if you want its UI value to persist across restarts.

---

## Option B — Blueprint + REST sensor

1. Create the feed sensor: copy the **Standard RSS 2.0** block from
   [`rss_rest_sensor_example.yaml`](rss_rest_sensor_example.yaml) into
   `configuration.yaml` (or a package), set your `resource:` URL, restart HA.
   Confirm the sensor has an **`item`** attribute in Developer Tools → States.
2. Download icon **85** on the AWTRIX **Icons** tab.
3. **Install the blueprint** — use whichever method you prefer:

   **Method 1 – Import from URL (easiest)**
   1. In Home Assistant go to **Settings → Automations & Scenes → Blueprints**.
   2. Click **Import Blueprint** (bottom-right).
   3. Paste this URL and click **Preview**, then **Import Blueprint**:
      ```
      https://github.com/tubalainen/awtrix3-homeassistant-blueprints/blob/main/RSS_feed/rss_feed_awtrix3.yaml
      ```
      Home Assistant fetches the file and adds it under *AWTRIX 3 – RSS Feed
      Headlines*. No restart needed.

   **Method 2 – Manual file copy**
   1. Download [`rss_feed_awtrix3.yaml`](rss_feed_awtrix3.yaml).
   2. Place it in your config folder under
      `config/blueprints/automation/awtrix3/rss_feed_awtrix3.yaml`
      (create the `awtrix3` subfolder if it doesn't exist).
   3. In **Settings → Automations & Scenes → Blueprints**, click the overflow
      menu (⋮) → **Reload Blueprints** (or restart HA). The blueprint now appears
      in the list.

4. **Create the automation:** on the blueprint's card click **Create
   Automation** (Method 1) or find it in the Blueprints list and click **Use
   Blueprint**, then fill in:

| Field | What to enter |
|-------|----------------|
| **AWTRIX MQTT topic prefix** | The prefix before `/custom/` (AWTRIX UI → *Network*). No trailing slash. |
| **RSS feed sensor** | The sensor from step 1. |
| **Number of headlines** | 1–20. |
| **Icon behaviour** | Fixed left / scroll-away (no reappear) / scroll-away (reappear). |
| **Icon** | Blank = RSS icon #85, or your own ID / filename / Base64. |
| **Text colour** | Hex, e.g. `#FFA500`. |
| **Headline separator** | Text shown between headlines. |
| **Safety re-push interval** | Minutes between safety re-sends. |

---

## How it works

Both options build an AWTRIX
[Custom App](https://blueforcer.github.io/awtrix3/#/api?id=custom-apps-and-notifications)
payload and publish it to `<prefix>/custom/rss`:

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
  `0` icon fixed left · `1` scrolls away, no reappear · `2` scrolls away, reappears each loop.
- `repeat: 1` scrolls the full set of headlines once, then the app advances to
  the next app in the AWTRIX loop — i.e. "show N headlines, then move on".

### Removing the app

Publish an **empty** payload to `<prefix>/custom/rss` (Developer Tools →
Actions → `mqtt.publish`).

---

## Notes & limitations

- The automations use the **modern HA automation syntax**
  (`triggers:`/`trigger:`/`actions:`/`action:`) and require **Home Assistant
  2024.10 or newer**.
- Home Assistant's REST integration auto-converts the feed's XML to a dict, so
  `value_json.rss.channel.item` is the item list. Atom feeds use
  `value_json.feed.entry` — see the variant in the REST sensor example.
- Icons are **not** auto-downloaded by ID at send time; add them via the AWTRIX
  web UI first.
- Titles are passed through `striptags` + trim to drop stray HTML.

### Editor warnings (VS Code / Studio Code Server)

When you paste the package in, the Home Assistant extension shows yellow
**"Entity … does not exist in your Home Assistant instance"** warnings for the
`input_*` / `sensor.awtrix_rss_feed` entities. That's expected — those entities
are *created by this very package*, so they don't exist until you **restart
Home Assistant**. After a restart the warnings clear.

The authoritative check is **Developer Tools → YAML → Check Configuration** in
Home Assistant itself (not the editor). If that passes, you're good.
