# Frequently Asked Questions

### Is this a standalone card, or does it need Bubble Card?

It's a **module** for [Bubble Card](https://github.com/Clooos/Bubble-Card) — Bubble Card must be installed first. See [Installation](installation.md).

### Is this available in HACS?

No, and this is by design. Bubble Weather Pro is a **Bubble Card YAML module** — not a frontend JavaScript resource, not a custom integration, and not a theme. HACS doesn't have a category that fits this type of project. The correct install method is Bubble Card's own built-in "Import module" URL, which is a single copy-paste step with no HACS entry required.

If you want to install Bubble Card itself, that's available in HACS under Frontend.

### Does it work with any weather integration?

Yes, in principle — anything exposing a standard `weather.*` entity. Feature completeness (hourly data, rain probability, etc.) depends on what your specific integration provides. See [Weather Providers](configuration.md#weather-providers).

### Do I need the Moon integration installed?

No. Without a configured `moon_entity`, the module calculates an approximate moon phase from the date. Add the built-in Moon integration only if you want the more precise, astronomically-sourced phase. See [Moon Integration](configuration.md#moon-integration).

### Can I use this on a wall-mounted tablet / kiosk dashboard?

Yes — for best performance on lower-powered devices, set `animated_icons: false` and `dynamic_background: false`. See [Performance](configuration.md#performance).

### Can I show multiple locations?

Not yet in a single card — add multiple Bubble Weather Pro cards, each pointed at a different `weather.*` entity (one per location/integration). A built-in location switcher is on the [roadmap](../README.md#-roadmap).

### Does it support imperial and metric units?

Yes — `temperature_unit: auto` (the default) follows your Home Assistant profile's unit system. You can force `°C` or `°F` explicitly regardless of profile. See [Configuration](configuration.md#weather_pro-options).

### Can I theme it to match my dashboard?

The module ships with its own gradient-based look by default (`dynamic_background: true`). Disabling that flag lets your active Home Assistant/Bubble Card theme's card background show through instead. Dedicated theme packs (dark, minimal, high-contrast, seasonal) are on the [roadmap](../README.md#-roadmap).

### Is this project affiliated with Bubble Card or Home Assistant?

No — this is an independent, community-maintained module built on top of Bubble Card's public module system. It isn't officially affiliated with the Bubble Card or Home Assistant core projects.

### How do I report a bug or request a feature?

See [CONTRIBUTING.md](../CONTRIBUTING.md) — use the [bug report](../.github/ISSUE_TEMPLATE/bug_report.md) or [feature request](../.github/ISSUE_TEMPLATE/feature_request.md) templates.

### What license is this under?

[MIT](../LICENSE) — free for personal and commercial use, with attribution appreciated but not required beyond the license terms.
