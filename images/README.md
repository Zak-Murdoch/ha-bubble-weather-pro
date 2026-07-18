# Images

This folder is referenced by the main [`README.md`](../README.md) and should contain the following real assets before (or shortly after) the public announcement of v1.0.0. None of these block the release — they're placeholders documented here so a contributor can fill them in.

| File | Used in | What to capture | Suggested size |
|---|---|---|---|
| `dashboard.png` | README banner | Full desktop view of the card in `apple-weather` mode, all sections visible, on a clean dashboard background | 1200×800+ (16:10 or wider) |
| `mobile.png` | README / docs | The `compact-mobile` example on an actual phone screen or narrow browser viewport | 750×1334 or similar phone aspect ratio |
| `animation.gif` | README | 5–10s screen recording showing icon animation and the hourly strip being scrolled | ≤ 8MB, 10–15fps is plenty for a GIF this length |

## How to capture

1. Set up a test dashboard using [`examples/apple-weather.yaml`](../examples/apple-weather.yaml).
2. Use your OS screenshot tool (macOS: `Cmd+Shift+4`, Windows: Snipping Tool, Linux: any) for the PNGs.
3. For the GIF, screen-record with QuickTime/OBS/ScreenToGif and convert to GIF with a tool like `gifski` or ezgif.com, keeping file size reasonable for a README.
4. Drop the files directly into this folder with the exact filenames above — the README and docs already reference them by path.

## Placeholder note

Until real assets are added, the README's image tags will render as broken images on GitHub. Adding these three files is the single highest-impact remaining polish item after the v1.0.0 release — see the "Remaining recommendations" section of the project handoff summary.
