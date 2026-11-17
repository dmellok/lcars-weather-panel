# LCARS weather panel

The Environmental and 7 Day Forecast sections of an LCARS-style Home Assistant dashboard built for a 6-colour e-ink panel in Tesserae.

**Live preview: https://dmellok.github.io/lcars-weather-panel/**

`index.html` is self-contained. Open it in a browser and it renders with sample data. It has no JavaScript dependencies; the only external request is the Antonio font from Google Fonts.

## What it shows

- Interior temperature as the hero figure, with a 24-hour trace drawn as rounded bars
- Exterior temperature, interior and exterior humidity, pressure, wind and UV index
- Seven days of high/low range bars, each with a condition pill and rainfall

## Using it in a Tesserae code element

1. Add a code element 1090 px wide (about 830 px tall) with `<div id="app"></div>` as its HTML.
2. Paste the contents of `<style>` into the CSS field and the contents of `<script>` into the JS field.
3. Cache the font once with `add_font("Antonio", weights=[400, 700])`.
4. Edit the `CFG` block at the top of the script to name your own entities.
5. Add three sources:

| name | key | options |
| --- | --- | --- |
| `ha` | `ha_service` | `{"scope": "states"}` |
| `thist` | `ha_service` | `{"scope": "history", "entity_id": "<your temperature sensor>", "hours": 24}` |
| `om` | `openmeteo_service` | `{"scope": "daily", "latitude": <lat>, "longitude": <lon>, "forecast_days": 7}` |

When `ctx.data.ha` is present the script uses it; otherwise it falls back to the built-in sample data.

## Colours

The block colours are the two-ink blends a Spectra 6 panel prints cleanly (orange `#FF8000`, amber `#FFBF00`, pink `#FF8080`, blush `#FFBFBF`, sky `#8C8CFF`). Type is kept to pure white, yellow or black so it stays crisp when dithered.
