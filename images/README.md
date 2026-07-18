# Images

Assets used in the README and documentation.

| File | Status | Dimensions | Description |
|---|---|---|---|
| `desktop.png` | ✅ included | 504 × 500 px | Desktop dashboard — current conditions, daily forecast, hourly strip |
| `mobile.png` | ✅ included | 800 × 1207 px | Mobile dashboard — full card with sun times, conditions, forecast, and hourly strip |
| `animation.gif` | 🔲 needed | ≤ 8 MB, 10–15 fps | Animated demo showing live icon animations and hourly strip scroll |

## How to capture the animation GIF

1. Set up a test dashboard using [`examples/apple-weather.yaml`](../examples/apple-weather.yaml).
2. Record a 5–10 s screen capture with QuickTime (macOS), OBS, or ScreenToGif (Windows).
3. Convert to GIF using `gifski` or [ezgif.com](https://ezgif.com) — optimise to keep the file under 8 MB (10–15 fps is plenty for a short loop).
4. Save as `images/animation.gif` — the README already references this path.

## Updating existing images

The images are PNG-optimised (stripped metadata, max compression). To replace:

1. Capture at the highest resolution available.
2. Run through ImageMagick to trim borders and compress:

   ```bash
   convert new-screenshot.png -fuzz 3% -trim +repage -define png:compression-level=9 -strip images/desktop.png
   ```

3. Commit as a separate `assets:` commit so the diff is easy to review.
