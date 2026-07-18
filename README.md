<div align="center">

<img src="images/dashboard.png" alt="Bubble Weather Pro banner" width="720">

# 🌤️ Bubble Weather Pro

**A premium, Apple Weather–inspired dashboard module for [Bubble Card](https://github.com/Clooos/Bubble-Card)**

[![Latest Release](https://img.shields.io/github/v/release/Zak-Murdoch/ha-bubble-weather-pro?style=for-the-badge&color=orange)](https://github.com/Zak-Murdoch/ha-bubble-weather-pro/releases/latest)
[![License](https://img.shields.io/github/license/Zak-Murdoch/ha-bubble-weather-pro?style=for-the-badge)](LICENSE)
[![Home Assistant](https://img.shields.io/badge/Home%20Assistant-2024.6%2B-41BDF5?style=for-the-badge&logo=home-assistant&logoColor=white)](https://www.home-assistant.io/)
[![Bubble Card](https://img.shields.io/badge/Bubble%20Card-2.0%2B-purple?style=for-the-badge)](https://github.com/Clooos/Bubble-Card)
[![GitHub Stars](https://img.shields.io/github/stars/Zak-Murdoch/ha-bubble-weather-pro?style=for-the-badge&color=yellow)](https://github.com/Zak-Murdoch/ha-bubble-weather-pro/stargazers)

[Installation](#-installation) • [Configuration](#-configuration) • [Examples](#-examples) • [FAQ](#-faq) • [Images](#️-images--assets) • [Roadmap](#️-roadmap) • [Contributing](#-contributing)

</div>

---

## ✨ Overview

**Bubble Weather Pro** transforms a standard Home Assistant weather entity into a beautiful, animated, Apple Weather–style dashboard card, built as a module for [Bubble Card](https://github.com/Clooos/Bubble-Card).

It's designed for people who want their weather dashboard to feel like a premium mobile app — not a raw data table.

> 📸 **Screenshot placeholder** — see [`images/dashboard.png`](images/dashboard.png). Replace with a real capture of your dashboard at 1200×800 or larger before release. See [Images](#-images--assets) below.

> 🎞️ **Animated GIF placeholder** — see [`images/animation.gif`](images/animation.gif). A 5–10s screen recording showing icon animation and hourly scroll works best.

---

## 🚀 Features

- 🎨 **Animated weather icons** — smooth, condition-aware icon animations (sun, clouds, rain, snow, storms, fog)
- 🌈 **Dynamic weather backgrounds** — background gradients/scenes shift with current conditions and time of day
- 📊 **Current conditions** — temperature, "feels like," condition text, and key metrics at a glance
- ⏱️ **Hourly forecast** — scrollable hour-by-hour strip
- 📅 **Daily forecast** — multi-day outlook with high/low and condition icons
- 🌅 **Sunrise & sunset** times
- 🌄 **First light & last light** (civil twilight) times
- 🌕 **Moon phase** display with optional dedicated moon entity
- 💨 **Wind** speed and direction
- 💧 **Humidity**
- ☔ **Rain probability**
- 📱 **Fully responsive layout** — desktop, tablet, and mobile dashboards
- 🧩 **Native Bubble Card module import** — installs like any other Bubble Card module, no custom card boilerplate

---

## 📦 Installation

### Requirements

| Requirement | Minimum version |
|---|---|
| Home Assistant | 2024.6+ |
| [Bubble Card](https://github.com/Clooos/Bubble-Card) | 2.0+ (installed via HACS) |
| A configured `weather.*` entity | any compatible integration — see [Supported Weather Integrations](#-supported-weather-integrations) |

### Step 1 — Install Bubble Card

If you don't already have Bubble Card installed:

1. In HACS, search for **Bubble Card** and install it.
2. Add the Bubble Card resource if HACS didn't do it automatically (**Settings → Dashboards → Resources**).

Full details: [Bubble Card installation guide](https://github.com/Clooos/Bubble-Card#installation).

### Step 2 — Import the Bubble Weather Pro module

Bubble Card supports **module import** directly from a URL — no manual file copying required.

1. Open any Bubble Card card in the dashboard editor.
2. Click **Manage modules → Import module**.
3. Paste this URL:

   ```
   https://raw.githubusercontent.com/Zak-Murdoch/ha-bubble-weather-pro/main/module/bubble-weather-pro.yaml
   ```

4. Click **Import**, then **Save**.

The module is now available to any Bubble Card "Pop-up" or "Button" card as **Bubble Weather Pro**.

> For a fully manual install (no internet import), see [`docs/installation.md`](docs/installation.md#manual-installation).

### Step 3 — Add the card

Add a new Bubble Card, choose the **Bubble Weather Pro** module, and point it at your weather entity:

```yaml
type: custom:bubble-card
card_type: pop-up
modules:
  - bubble-weather-pro
entity: weather.home
```

See [`examples/`](examples/) for full working dashboards, and [`docs/configuration.md`](docs/configuration.md) for every option.

---

## ⚙️ Configuration

Minimal example:

```yaml
type: custom:bubble-card
card_type: pop-up
modules:
  - bubble-weather-pro
entity: weather.home
```

Full example with optional entities and overrides:

```yaml
type: custom:bubble-card
card_type: pop-up
modules:
  - bubble-weather-pro
entity: weather.home
weather_pro:
  moon_entity: sensor.moon_phase
  sun_entity: sun.sun
  show_hourly: true
  hourly_hours: 12
  show_daily: true
  daily_days: 7
  show_wind: true
  show_humidity: true
  show_rain_probability: true
  animated_icons: true
  dynamic_background: true
  temperature_unit: auto
  first_last_light: true
```

Every option, its default, and worked examples are documented in **[`docs/configuration.md`](docs/configuration.md)**.

---

## 🖼️ Examples

Ready-to-use dashboard YAML lives in [`examples/`](examples/):

| File | Description |
|---|---|
| [`minimal.yaml`](examples/minimal.yaml) | Smallest possible working config |
| [`simple-card.yaml`](examples/simple-card.yaml) | A standard single-entity weather card |
| [`apple-weather.yaml`](examples/apple-weather.yaml) | Full Apple Weather–style layout with all sections enabled |
| [`full-dashboard.yaml`](examples/full-dashboard.yaml) | Weather module inside a complete example dashboard view |
| [`compact-mobile.yaml`](examples/compact-mobile.yaml) | Condensed layout tuned for phone-sized dashboards |

---

## 🌦️ Supported Weather Integrations

Bubble Weather Pro works with **any** integration that exposes a standard `weather.*` entity supporting the Home Assistant `weather` platform forecast services, including:

- Met.no (built-in, no API key)
- OpenWeatherMap
- AccuWeather
- Pirate Weather
- Tomorrow.io
- WeatherFlow / Tempest
- Ecobee weather
- National Weather Service (NWS, US)

Anything that provides `forecast_daily` / `forecast_hourly` data via the `weather.get_forecasts` service will populate the daily and hourly sections automatically. See [`docs/configuration.md#weather-providers`](docs/configuration.md#weather-providers) for provider-specific notes and known quirks.

---

## 🌕 Optional Moon Integration

The moon phase panel works out of the box using Home Assistant's built-in **Moon** integration (`sensor.moon_phase` after enabling it under **Settings → Devices & Services → Add Integration → Moon**).

If you don't configure a moon entity, the module falls back to a calculated moon phase using sun/date data — no extra integration required. See [`docs/configuration.md#moon-integration`](docs/configuration.md#moon-integration).

---

## 🛠️ Troubleshooting

Common issues and fixes now live in **[`docs/troubleshooting.md`](docs/troubleshooting.md)**, covering:

- Module not appearing in Bubble Card's module list
- Icons not animating
- Forecast sections empty
- Wrong sunrise/sunset or twilight times
- Layout breaking on small screens

## ❓ FAQ

See **[`docs/faq.md`](docs/faq.md)** for answers to the most common questions, including licensing, HACS support, theming, and multi-location setups.

---

## 🖼️ Images & Assets

The three assets below are referenced throughout this README and the docs. They are not yet included in the repository — adding them is the single highest-impact remaining polish item after the v1.0.0 release.

| File | Used in | What to capture | Suggested dimensions |
|---|---|---|---|
| `images/dashboard.png` | README banner | Full desktop view of the card in `apple-weather` mode, all sections visible | 1200 × 800 px or larger |
| `images/mobile.png` | README / docs | `compact-mobile` example on a phone screen or narrow viewport | 750 × 1334 px or phone aspect ratio |
| `images/animation.gif` | README | 5–10 s recording of icon animation and hourly strip scrolling | ≤ 8 MB, 10–15 fps |

**How to add them:**

1. Set up a test dashboard using [`examples/apple-weather.yaml`](examples/apple-weather.yaml).
2. Capture PNGs with your OS screenshot tool.
3. Record and convert a GIF with QuickTime, OBS, ScreenToGif, or similar — then optimise with `gifski` or [ezgif.com](https://ezgif.com) to keep the file size reasonable.
4. Drop files directly into the `images/` folder using the exact filenames above — the README and docs already reference them by path.

See [`images/README.md`](images/README.md) for more detail.

---

## 🗺️ Roadmap

Planned for future releases — see [open issues](https://github.com/Zak-Murdoch/ha-bubble-weather-pro/issues) to vote or contribute:

- [ ] 📡 Radar overlay
- [ ] ☀️ UV index
- [ ] 🌫️ Air quality index
- [ ] 🤧 Pollen count
- [ ] 🌡️ Barometric pressure trend
- [ ] ⚠️ Weather alerts / warnings banner
- [ ] 📍 Multiple locations / location switcher
- [ ] 🎨 Theme packs (dark, minimal, high-contrast, seasonal)
- [ ] 📈 Interactive historical/forecast charts
- [ ] 🌀 Additional weather animations (hail, sleet, dust)
- [ ] 🌍 Localisation / i18n for labels and units

Vote, comment, or track progress on any of the above in the [issues list](https://github.com/Zak-Murdoch/ha-bubble-weather-pro/issues). Completed milestones are recorded in [`CHANGELOG.md`](CHANGELOG.md).

---

## 🤝 Contributing

Contributions are welcome — bug reports, features, docs, and translations alike. Please read **[`CONTRIBUTING.md`](CONTRIBUTING.md)** before opening a pull request, and check the **[Code of Conduct](CODE_OF_CONDUCT.md)**.

## 🔒 Security

Found a security issue? Please see **[`SECURITY.md`](SECURITY.md)** for how to report it responsibly.

## 🙏 Acknowledgements

- [Bubble Card](https://github.com/Clooos/Bubble-Card) by [Clooos](https://github.com/Clooos) — the module framework this project builds on
- [Home Assistant](https://www.home-assistant.io/) and its weather integration maintainers
- The Home Assistant community for testing, feedback, and icon/animation inspiration

## 📄 License

Released under the [MIT License](LICENSE).

</div>
