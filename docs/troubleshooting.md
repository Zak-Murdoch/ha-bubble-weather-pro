# Troubleshooting

## Module doesn't appear in Bubble Card's module list

1. Confirm the import succeeded: **Manage modules** should list **Bubble Weather Pro**. If it doesn't, re-import using the exact raw URL from [`README.md`](../README.md#-installation).
2. Hard-refresh your browser (Ctrl/Cmd+Shift+R) — module lists are cached client-side.
3. Confirm Bubble Card itself is up to date (2.0+) — module import support requires a recent Bubble Card version.
4. Check **Settings → Dashboards → Resources** for a `bubble-card.js` entry with no version-mismatch warnings.

## Icons not animating

- Check `weather_pro.animated_icons` is `true` (or unset, since it defaults to `true`).
- Some browsers/embedded WebViews (older tablet dashboards, some kiosk browsers) disable CSS animations to save power — this is a browser-level setting, not something the module controls.
- If performance is the concern rather than a bug, this is expected/recommended behaviour on low-powered devices — see [Performance](configuration.md#performance).

## Forecast sections empty (hourly or daily)

This is almost always one of:

1. **Your weather integration doesn't provide that forecast type.** Check **Developer Tools → Actions**, call `weather.get_forecasts` with `type: hourly` (or `daily`) against your entity, and confirm data comes back. If it doesn't, the integration itself doesn't support it — this isn't a module issue.
2. **Stale entity state.** Some integrations only populate forecasts after their first poll interval. Wait a few minutes after adding the integration, or check the integration's own logs.
3. **`show_hourly`/`show_daily` explicitly set to `false`.** Check your config.

## Wrong sunrise/sunset or first/last light times

- Confirm `sun_entity` (default `sun.sun`) is the entity you expect — if you have a custom or duplicated sun entity, point `weather_pro.sun_entity` at the right one explicitly.
- Times shown are in your Home Assistant instance's configured time zone (**Settings → System → General**); if that's wrong, fix it there rather than in the module config.
- First/last light needs `next_dawn`/`next_dusk`-equivalent attributes on the sun entity — a heavily modified custom sun entity may not expose these, in which case that row won't render (see [Known Limitations](configuration.md#known-limitations)).

## Layout breaking on small screens / cards

- Try the tuned [`examples/compact-mobile.yaml`](../examples/compact-mobile.yaml) config as a baseline.
- Very narrow columns (e.g. a 1-column mobile dashboard with heavy sidebar padding) can push the card below the ~400px "mobile" breakpoint threshold even on larger phones — this is expected, and the compact layout is designed for exactly that case.
- If a specific dashboard theme is overriding card padding/border-radius in a way that clips content, test with the default Home Assistant theme to isolate whether it's a theme conflict.

## Nothing shows / card is blank

1. Open the browser console (F12 → Console) and look for JavaScript errors mentioning `bubble-weather-pro` or `bubble-card`.
2. Confirm `entity:` points at a real `weather.*` entity (**Developer Tools → States**, filter by `weather.`).
3. Try the [minimal example](../examples/minimal.yaml) as a baseline — if that also fails, the issue is environmental (Bubble Card install, resource caching) rather than a config mistake.

## Still stuck?

- Check the [FAQ](faq.md).
- Search [existing issues](https://github.com/Zak-Murdoch/ha-bubble-weather-pro/issues) — your problem may already be reported.
- Open a new [bug report](https://github.com/Zak-Murdoch/ha-bubble-weather-pro/issues/new?template=bug_report.md) with your config, versions, and console errors as described in [CONTRIBUTING.md](../CONTRIBUTING.md#reporting-bugs-effectively).
