# Contributing to Bubble Weather Pro

Thanks for considering a contribution — whether it's a bug report, a new feature, a doc fix, or a translation, it's genuinely welcome.

## Before you start

- Check [open issues](https://github.com/Zak-Murdoch/ha-bubble-weather-pro/issues) and the [roadmap](README.md#-roadmap) to avoid duplicate work.
- For anything non-trivial (new feature, breaking change), please open an issue first to discuss the approach before writing code.
- Read the [Code of Conduct](CODE_OF_CONDUCT.md) — we expect all contributors to follow it.

## Ways to contribute

- 🐛 **Bug reports** — use the [bug report template](.github/ISSUE_TEMPLATE/bug_report.md)
- 💡 **Feature requests** — use the [feature request template](.github/ISSUE_TEMPLATE/feature_request.md)
- 📝 **Documentation** — fixes, clarifications, and examples in `docs/` and `README.md`
- 🧩 **Example dashboards** — new configs in `examples/`
- 🌍 **Localisation** — help translate labels once i18n support lands (see roadmap)
- 💻 **Code** — improvements to `module/bubble-weather-pro.yaml`

## Development setup

1. Fork and clone the repository.
2. Install [Home Assistant](https://www.home-assistant.io/installation/) (a local dev instance or a test VM/container is ideal — don't develop against a production instance).
3. Install [Bubble Card](https://github.com/Clooos/Bubble-Card) via HACS.
4. Import your local copy of `module/bubble-weather-pro.yaml` into a test dashboard (Bubble Card → Manage modules → Import module → paste the raw file contents, or point at your fork's raw URL on a branch).
5. Use one of the files in `examples/` as your starting dashboard config.

## Making changes

- Keep the module's YAML readable — comment non-obvious template logic.
- Don't introduce breaking config changes without a clear migration note in `CHANGELOG.md` and a mention in the PR description.
- Match existing naming conventions for config keys (`snake_case`, grouped under `weather_pro:`).
- Test against at least one real `weather.*` entity before submitting (Met.no is a good zero-setup option).
- Update relevant docs (`docs/configuration.md`, `README.md`) alongside any config option changes.

## Commit style

We use short, conventional-style commit messages:

```
docs: clarify moon integration fallback behaviour
fix: correct wind direction rounding
feat: add compact mobile layout variant
ci: bump yaml validation action version
```

## Submitting a pull request

1. Create a branch from `main`: `git checkout -b feat/short-description`.
2. Make your changes and test them in a real (or test) Home Assistant instance.
3. Fill out the [pull request template](.github/PULL_REQUEST_TEMPLATE.md) completely — screenshots/GIFs for anything visual are extremely helpful.
4. Ensure CI (Markdown lint + YAML validation) passes.
5. One maintainer review and approval is required before merge.

## Reporting bugs effectively

The more of this you include, the faster a fix happens:

- Home Assistant version
- Bubble Card version
- Your weather integration (e.g. Met.no, OpenWeatherMap)
- Your `weather_pro:` config block
- Browser/app and device (desktop, iOS app, Android app, tablet)
- Screenshot or screen recording of the issue
- Relevant browser console errors (F12 → Console)

Thanks again for helping make this project better for the whole Home Assistant community.
