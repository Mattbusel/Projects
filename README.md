# Weather-Based Camera Settings Recommender

A small Python script that looks up the current weather for a city on OpenWeatherMap and emails you suggested camera settings (ISO, aperture, shutter speed, white balance, tips) for shooting in those conditions.

An early 2024 learning project: one working script plus two unfinished experiments.

## What it does

`photo.py`:

1. Asks for a city name and a recipient email address.
2. Fetches current conditions from the OpenWeatherMap current-weather API (metric units).
3. Picks settings from simple rules keyed on the weather description (clear, clouds, rain or drizzle, snow, anything else) and, for clear skies, visibility.
4. Sends the weather summary and the suggestions by email over Gmail SMTP (STARTTLS on port 587).

## Quick start

```bash
pip install requests flask   # flask is imported by photo.py, though not used yet

export OPENWEATHERMAP_API_KEY=your_key
export EMAIL_ADDRESS=you@gmail.com
export EMAIL_PASSWORD=your_app_password   # a Gmail app password, not your account password

python photo.py
```

On Windows use `set NAME=value` instead of `export`.

## Files

| Path | What it is |
|---|---|
| `photo.py` | The working script described above |
| `UI.html` | Start of a Flask web front end. Despite the extension it is Python, and it is incomplete (undefined variables, missing templates) |
| `Camera API Connect.py` | Start of a Canon EDSDK binding through `cffi`. Incomplete; it does not run |
| `build/`, `dist/` | PyInstaller output for `photo.py` (Windows) |

## Known limitations

- Some ISO ranges are written as arithmetic (`200 - 400`), so the email shows a negative number instead of a range for cloudy, rainy and snowy weather.
- The rules are general rules of thumb; adjust for your camera and scene.
- The SMTP host is hard-coded to Gmail.
