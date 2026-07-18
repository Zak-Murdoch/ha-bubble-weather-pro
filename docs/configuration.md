# Configuration Reference

All Bubble Weather Pro options live under a `weather_pro:` block on the Bubble Card, alongside the standard Bubble Card / module fields (`entity`, `modules`, `name`, `icon`, etc.).

```yaml
type: custom:bubble-card
card_type: pop-up
modules:
  - bubble-weather-pro
entity: weather.home     # required — your weather entity
weather_pro:
  # ...options below...
```

## Core fields (outside `weather_pro:`)

| Option | Type | Default | Description |
|---|---|---|---|
| `entity` | string | — | **Required.** A `weather.*` entity providing current conditions and forecasts. |
| `modules` | list | — | Must include `bubble-weather-pro`. |
| `name` | string | entity friendly name | Overrides the card title. |
| `icon` | string | entity default icon | Overrides the icon shown in collapsed/button views. |

## `weather_pro:` options

| Option | Type | Default | Description |
|---|---|---|---|
| `moon_entity` | string (entity id) | `null` | A `sensor.*` moon phase entity (e.g. from the built-in **Moon** integration). If omitted, phase is calculated from date/sun data. See [Moon Integration](#moon-integration). |
| `sun_entity` | string (entity id) | `sun.sun` | Sun entity used for sunrise/sunset and first/last light calculations. |
| `show_hourly` | boolean | `true` | Show the scrollable hourly forecast strip. |
| `hourly_hours` | number (4–24) | `12` | How many hours to display in the hourly strip. |
| `show_daily` | boolean | `true` | Show the daily forecast list. |
| `daily_days` | number (1–10) | `7` | How many days to display (capped by what your weather integration provides — most support 5–10). |
| `show_wind` | boolean | `true` | Show wind speed and direction. |
| `show_humidity` | boolean | `true` | Show relative humidity. |
| `show_rain_probability` | boolean | `true` | Show precipitation probability, when the integration provides it. |
| `first_last_light` | boolean | `true` | Show first light / last light (civil twilight), in addition to sunrise/sunset. |
| `animated_icons` | boolean | `true` | Enable icon animation (subtle float/drift, condition-specific motion). Disable for a static, battery-friendlier look on low-powered tablets. |
| `dynamic_background` | boolean | `true` | Enable the background gradient/scene that shifts with condition and day/night. Disable to use your dashboard theme's default background instead. |
| `temperature_unit` | string: `auto` \| `°C` \| `°F` | `auto` | `auto` follows your Home Assistant profile unit system. Override to force a specific unit regardless of profile. |

### Example: every option set explicitly

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
  hourly_hours: 24
  show_daily: true
  daily_days: 10
  show_wind: true
  show_humidity: true
  show_rain_probability: true
  first_last_light: true
  animated_icons: true
  dynamic_background: true
  temperature_unit: auto
```

## Weather Providers

Bubble Weather Pro reads from whatever your `weather.*` entity exposes via `weather.get_forecasts` (or legacy `forecast` attributes on older integrations). Notes on common providers:

| Provider | Hourly forecast | Daily forecast | Rain probability | Notes |
|---|---|---|---|---|
| Met.no (built-in) | ✅ | ✅ | ✅ | No API key needed; great zero-config default. |
| OpenWeatherMap | ✅ | ✅ | ✅ | Requires API key; free tier has request limits. |
| AccuWeather | ✅ | ✅ | ✅ | Requires API key. |
| Pirate Weather | ✅ | ✅ | ✅ | Drop-in alternative to the (paid) Dark Sky API. |
| Tomorrow.io | ✅ | ✅ | ✅ | Requires API key; generous free tier. |
| National Weather Service (NWS) | ✅ | ✅ | ⚠️ varies | US only; some fields depend on station coverage. |
| Ecobee weather | ⚠️ limited | ✅ | ❌ | Daily-only in most setups. |

If your provider doesn't expose hourly or rain-probability data, the corresponding section/metric is simply hidden — set `show_hourly: false` / `show_rain_probability: false` explicitly if you'd rather not rely on auto-hiding.

## Forecast Entities

Since Home Assistant 2023.9, forecasts are fetched via the `weather.get_forecasts` service rather than static entity attributes. Bubble Weather Pro handles both patterns automatically — no configuration needed either way. If your daily/hourly sections are empty, see [Troubleshooting](troubleshooting.md#forecast-sections-empty).

## Moon Integration

- **With `moon_entity` set**: the module reads phase state directly (`new_moon`, `waxing_crescent`, `first_quarter`, etc. — matching Home Assistant's built-in [Moon integration](https://www.home-assistant.io/integrations/moon/) states).
- **Without `moon_entity`**: phase is calculated from the current date, giving a reasonable approximation without requiring you to add the Moon integration.

To enable the native integration: **Settings → Devices & Services → Add Integration → Moon**, then reference the resulting `sensor.moon_phase` (or your renamed entity id) as `moon_entity`.

## Responsive Behaviour

The module targets three layout tiers, adjusting automatically based on the rendered card width (not the device width, so it also adapts correctly inside narrow dashboard columns or split views):

| Breakpoint | Approx. width | Behaviour |
|---|---|---|
| Desktop | > 600px | Full layout — all sections, wide hourly strip, 2–3 column metrics |
| Tablet | 400–600px | Slightly condensed spacing, hourly strip remains scrollable |
| Mobile | < 400px | Compact spacing, metrics collapse to a 2-column grid, larger touch targets |

See [`examples/compact-mobile.yaml`](../examples/compact-mobile.yaml) for a config tuned specifically for small screens.

## Animations

`animated_icons: true` enables condition-aware motion:

- Sun/clear — gentle glow pulse
- Clouds — slow horizontal drift
- Rain/showers — falling drop animation
- Snow — falling flake animation
- Thunderstorms — flash/flicker on the icon
- Fog/mist — soft opacity pulse

Set `animated_icons: false` for a fully static card — recommended on older tablets (e.g. wall-mounted dashboard panels) where continuous animation can affect performance or battery life.

## Performance

- Disabling `dynamic_background` and `animated_icons` reduces continuous repaint/animation work — recommended for always-on wall panels.
- Lower `hourly_hours` and `daily_days` reduce the number of rendered forecast entries; the practical ceiling is usually your weather provider's own forecast range (e.g. Met.no provides up to ~10 days), not the module itself.

## Known Limitations

- Rain probability depends entirely on the underlying integration providing it — not all do.
- First/last light (civil twilight) requires the `sun.sun` entity's `next_dawn`/`next_dusk`-style attributes; a heavily customized or third-party sun entity may not expose these.
- The module does not fetch its own weather data — it only renders what your configured `weather.*` entity provides. Data-source issues (wrong location, stale forecast) are integration-level, not module-level.

See [Troubleshooting](troubleshooting.md) for fixes to specific issues, and [FAQ](faq.md) for common questions.
