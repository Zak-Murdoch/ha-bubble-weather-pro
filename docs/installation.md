# Installation

## Requirements

| Requirement | Minimum version |
|---|---|
| Home Assistant | 2024.6+ |
| [Bubble Card](https://github.com/Clooos/Bubble-Card) | 2.0+ |
| A `weather.*` entity | any provider with `forecast_daily`/`forecast_hourly` support recommended |

## 1. Install Bubble Card

Bubble Weather Pro is a **module** for Bubble Card, not a standalone card — Bubble Card must be installed first.

1. In HACS → **Frontend**, search for **Bubble Card** and install it.
2. Restart Home Assistant if prompted, and hard-refresh your browser (Ctrl/Cmd+Shift+R).
3. Confirm the resource was added: **Settings → Dashboards → ⋮ → Resources** should list `bubble-card.js`.

## 2. Import the module (recommended)

Bubble Card supports importing modules directly from a URL:

1. Add or edit a Bubble Card (`card_type: pop-up` or `button`) on any dashboard.
2. In the visual editor, open **Manage modules → Import module**.
3. Paste:

   ```text
   https://raw.githubusercontent.com/Zak-Murdoch/ha-bubble-weather-pro/main/module/bubble-weather-pro.yaml
   ```

4. Click **Import** — the module now appears as **Bubble Weather Pro** in the module list for every Bubble Card on this dashboard.
5. Select it, assign your `weather.*` entity, and **Save**.

## Manual installation

If you prefer not to import from a URL (offline installs, air-gapped systems, or you want to pin an exact commit):

1. Download [`module/bubble-weather-pro.yaml`](../module/bubble-weather-pro.yaml) from this repository.
2. In the Bubble Card module editor, choose **Manage modules → Add module → Paste YAML**, and paste the file's contents directly instead of importing by URL.
3. Save.

## 3. Add the card to a dashboard

Switch a dashboard view to **YAML mode** (⋮ → Edit Dashboard → ⋮ → Edit in YAML) and add:

```yaml
type: custom:bubble-card
card_type: pop-up
modules:
  - bubble-weather-pro
entity: weather.home
```

Or use the visual editor: **Add Card → Custom: Bubble Card → Pop-up**, then select the **Bubble Weather Pro** module and your weather entity from the dropdowns.

See [`examples/`](../examples/) for complete, copy-pasteable configurations.

## Updating

### If imported by URL

Re-open **Manage modules → Bubble Weather Pro → Update module** whenever a new release is available — this re-pulls the `main` branch copy. Check the [Releases page](https://github.com/Zak-Murdoch/ha-bubble-weather-pro/releases) or [`CHANGELOG.md`](../CHANGELOG.md) for what changed before updating, especially for major versions which may include breaking config changes.

### If installed manually

Download the updated `module/bubble-weather-pro.yaml` from the relevant [release tag](https://github.com/Zak-Murdoch/ha-bubble-weather-pro/releases) and replace your pasted module content.

## Uninstalling

1. Remove any `modules: [bubble-weather-pro]` references from your dashboard cards.
2. **Manage modules → Bubble Weather Pro → Remove module**.
3. Optionally uninstall Bubble Card itself via HACS if no longer needed.

## Next steps

- [Configuration reference](configuration.md) — every option, default, and example
- [Troubleshooting](troubleshooting.md) — fixes for common install/display issues
- [FAQ](faq.md)
