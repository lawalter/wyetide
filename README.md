<p align="center">
  <svg width="120" height="120" viewBox="0 0 48 48" fill="none" stroke="#61d3ba" stroke-width="5" stroke-linecap="round" stroke-linejoin="round" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="Wye Tide wave logo">
    <path d="M4 30 C 8 20, 16 10, 27 10 C 36 10, 41 16, 41 23 C 41 29, 36 32, 31 32 C 26 32, 23 28, 24 24 C 25 21, 28 20, 31 22"/>
    <path d="M6 37 C 12 34, 16 40, 22 37 C 28 34, 32 40, 38 37 C 40 36, 41 36, 43 37"/>
  </svg>
</p>

<h1 align="center">Wye Tide</h1>

<p align="center"><a href="https://lawalter.github.io/wyetide">lawalter.github.io/wyetide</a></p>

<p align="center">⛈️ ❄️ 💧 🌦️ 🌧️ 🌫️ 💨 🔥 🧊 ☁️ 🌥️ ⛅ ☀️ 🌙</p>

Wye Tide is a personal weather dashboard for select locations around the Chesapeake Bay, showing real-time weather conditions, air quality, UV index, tide data, and sun & moon times. It is one self-contained `index.html` with no framework or server. The dashboard pulls live data from public data sources and displays current conditions in a minimalist layout themed after a lightning bug. 

AI is raving:
> *"This thing actually has EPA compliance comments, two AQI data sources with an intelligent fallback, a luminance-based badge contrast helper, proper NWS alert pass-through, moon phase math, and an umbrella that reasons about time windows."* - Claude

## Overview

The [Wye Tide](https://lawalter.github.io/wyetide) dashboard includes:
- **🌤️ Weather** — the current conditions with a matching emoji, temperature, humidity, wind, gusts, precipitation potential, severe weather alerts, and more!
- **🌅 Sun and Moon** — first light, sunrise, sunset, and last light; tonight's moon is shown as an icon with illumination percentage matching the current phase.
- **🌫️ Air Quality** — the US AQI with today's forecasted peak, the highest reading so far, PM2.5, PM10, and ozone.
- **😎 UV Index** — the current UV index, a sparkline of the whole day's curve, solar noon, and estimated "burn time".
- **🌊 Tides** — tide predictions (for areas with a nearby station).

For select locations in:

- **Maryland** - Chesapeake Beach, Edgewater, Huntingtown, Patuxent NWR, Upper Marlboro, and Wye Island NRMA
- **Virginia** - Virginia Beach
- **Washington, DC** - Smithsonian

## Dive in!

Wye Tide is deployed via GitHub Pages at <a href="https://lawalter.github.io/wyetide">lawalter.github.io/wyetide</a>. 

To view locally, download `index.html` and open it in a browser. No API keys are required for weather, UV, sun, moon, or tides. The preferred air quality index data source requires an [Optional AirNow API Key](#optional-airnow-api-key), but the dashboard will also work without it (using Open-Meteo as default).

## Data sources

All data belongs to its provider and is subject to that provider's terms, independently of this project's license. The full, per-source obligations are documented in [`DISCLAIMER.md`](DISCLAIMER.md) and in a compliance comment block at the top of the script in `index.html`. Forecast values and advisory statements are selected and formatted, but never reworded or re-derived. 

| Data | Source | Notes |
|---|---|---|
| 🌤️ Weather &amp; alerts | [NOAA / National Weather Service](https://api.weather.gov) | US Government work, public domain |
| 🌫️ Air quality (without key) | [Open-Meteo](https://open-meteo.com) | CC&nbsp;BY&nbsp;4.0 — modeled AQI + pollutant levels |
| 🟢 Air quality (with key) | [EPA AirNow](https://www.airnow.gov/) | Preliminary data; credits the reporting agencies |
| 😎 UV index | [Open-Meteo](https://open-meteo.com) | CC&nbsp;BY&nbsp;4.0 |
| 🌅 Sun &amp; solar times | [sunrise-sunset.org](https://sunrise-sunset.org/) | Free &amp; keyless |
| 🌊 Tides | [NOAA CO-OPS](https://tidesandcurrents.noaa.gov/) | Official NOS predictions, public domain |

## Weather conditions

### 🌡️ Current temperature

The Weather card displays a big number, which is either the current **air temperature**, **wind chill** when it's cold and windy, or **heat index** when it's hot and humid. Values come from the nearest NWS observation station and are converted to degrees Fahrenheit. A [color-coded](#colors-) category descriptor is added below the value to quickly impress the temperature to users. Since stations can post partial readings, the dashboard will find the most recent value to report if the latest data doesn't contain an update.

### ⚠️ Hazards 

NWS alerts (watches, warnings, advisories) are included in the Weather card whenever there is an active hazard. An active alert shows the hazard name (e.g., "Coastal Flood Advisory") as a clickable link that opens a full description in a new tab. Hazard pages report complete details, including: headline, severity, urgency, affected area, when it's effective, and when it expires. Hazard information is never paraphrased. If the alert feed can't be reached, a "Hazards unavailable" message will be returned.

### ☔ The umbrella 

An umbrella icon appears next to the Weather card's high/low daily temperatures in the upper right hand corner whenever rain looks likely. The dashboard determines "likely rain" by finding any forecast from now until 10pm with an hourly precipitation chance of **30% or more** from the NWS. Hours that have already passed don't count, so the umbrella reflects the day ahead. It's just a friendly reminder to bring an umbrella on days that might call for one!

### 🌧️ Estimated rainfall and snow accumulation

When there's a chance of precipitation, the Weather card estimates how much. The NWS doesn't provide this as a number — it writes a sentence like *"New rainfall amounts between a tenth and quarter of an inch, except higher amounts possible in thunderstorms"* — so the card reads that prose and translates the words into inches:

- Rain, sleet, or freezing rain is reported as an **Estimated rainfall** row, e.g. `0.1-0.25 in`.
  - If the forecast warns that thunderstorms could bring more (*"except higher amounts possible in thunderstorms"*), the value picks up a `+`, like `0.1-0.25+ in`.
- Snow is reported as an **Estimated accumulation** row, e.g. `1-3 in`.
- **"Less than"** forecasts read as `<0.1 in`.
- The estimate row is excluded if a forecast is phrased in a way the dashboard can't parse, or if the forecast says something like *"little or no accumulation expected"*.

### 📏 Other metrics

- **High / low** — today's forecasted high and tonight's forecasted low temperatures are placed in the top right corner.
- **Conditions** — a short description of the current weather is included under the main temperature.
- **Air temperature** — only included if wind chill or heat index differ from air temperature.
- **Humidity** — relative humidity.
- **Wind** — sustained wind speed and direction.
- **Gusts** — gust speed (shows as "None" when the station reports no gust).
- **Chance of rain / snow / sleet** — changes title depending on the forecast; precipitation probability reported as a percentage.
- **Cloud cover** — Clear, Few, Scattered, Broken, Overcast, or Obscured, taken from the observation's reported cloud layers (the densest layer wins).
- **Pressure** — barometric pressure in inHg with a trend arrow (↑ rising, ↓ falling, → steady over the last ~3 hours). Falls back to sea-level pressure at stations that don't report raw barometric pressure.

### 📆 Six-day forecast

Below the current conditions, the Weather card shows a compact 6-day forecast starting with tomorrow's date. Each box contains the weekday, date, an emoji, forecasted high, forecasted low, and a raindrop emoji with the day's chance of precipitation (shown only when there's actually a chance). 

### 🌅 Sun times

First light, sunrise, sunset, and last light times are shown for today.

### 🌙 Moon phase

Computed from a known new-moon reference date and the 29.53-day lunar cycle. The dashboard works out the moon's current age, names the phase (New, Waxing Crescent, First Quarter, and so on), and calculates the illumination percentage with a cosine curve. A moon icon is drawn to match that illumination.

### 😄 Emojis
A little emoji beside the Weather card header is the current location's conditions at a glance, translated from the official NWS forecast icon. Hover over to view a description via tooltip. Here are all of the possible Weather emojis:

| Emoji | Means |
|---|---|
| ⛈️ | Thunderstorms |
| ❄️ | Snow |
| 💧 | Sleet or freezing rain |
| 🌦️ | Showers |
| 🌧️ | Rain |
| 🌫️ | Fog, haze, smoke, or dust |
| 💨 | Windy |
| 🔥 | Hot |
| 🧊 | Cold |
| ☁️ | Overcast |
| 🌥️ | Mostly cloudy |
| ⛅ | Partly cloudy |
| ☀️ | Clear (by day) |
| 🌙 | Clear (at night) |

A few of these are time-aware: **clear** skies show a sun ☀️ by day and a moon 🌙 by night, and both **partly** ⛅ and **mostly cloudy** 🌥️ quietly swap to a plain cloud ☁️ after dark. Since some conditions overlap in the raw forecast data, emojis are ranked hierarchically. For example, thunderstorms outrank plain rain, and snow outranks sleet. This system allows users to get the most meaningful takeaway from a single glyph.

## Air Quality 🌫️ 

The US Air Quality Index and the pollutants behind it are included in the Air Quality card. Data are sourced from **EPA AirNow** when an API key is configured, and **Open-Meteo**'s modeled air quality otherwise. EPA AirNow is considered to be more accurate in measuring wildfire smoke pollution. Open-Meteo models AQI over a roughly 40 km grid, so is more generalized. Hover over the info icon in the top right of the card to read a description of the Air Quality and find which source is being used. 

- **AQI** — current US AQI, [color-coded](#colors-) for severity.
- **Forecast** — today's predicted peak AQI (the "how bad will it get" number).
- **Max (time)** — the highest AQI actually recorded so far today, with the hour it happened.
- **PM2.5 / PM10 / Ozone** — the pollutant concentrations, each with a colored severity dot on the same scale as the AQI badge.

### Optional AirNow API key

Out of the box, the Air Quality card runs on Open-Meteo. To use data from EPA monitor data, obtain and configure an AirNow API key:

1. Request an API key for free at <https://docs.airnowapi.org/account/request/>.
2. Open `airnow-key.js` and paste it in: `window.AIRNOW_KEY = 'your-key-here';`

**The key lives in `airnow-key.js` on purpose — never in `index.html`.** See [Licensing](#licensing) below for why.

## UV Index 😎

The UV Index card contains important information helpful in mitigating sun exposure risk. Sun exposure information is sourced from **Open-Meteo** and solar noon is from **sunrise-sunset.org**. Hover over the info icon in the top right of the card to read sun protection advice applicable to the day's peak.

- **UV Index** — current UV index, [color-coded](#colors-) for severity.
- **Sparkline** — a little graph of the day's UV curve, with a marker on the current hour.
- **Max (time)** — the day's peak UV and when it hits.
- **Solar noon** — when the sun is highest (and UV strongest).
- **Burn time** — a rough estimate of how long until unprotected skin would burn at the current UV. Reports "No risk" when UV is negligible (e.g., at night).

## Tide 🌊 

High and low tide predictions are shown for locations with a nearby station in the Tide card. Locations without a tide station display a "No tidal station" message.

- **Current tide** — whether the water is Rising (incoming) or Falling (outgoing) right now, based on which comes next.
- **Next high tide** — the time of the next high (with "(tmrw)" if it's after midnight).
- **Next low tide** — the time of the next low, (with "(tmrw)" if it's after midnight).

## Colors 🎨

The Air Quality Index colors use the EPA's [ColorVision Assist](https://document.airnow.gov/technical-assistance-document-for-the-reporting-of-daily-air-quailty.pdf) palette (AQI Technical Assistance Document, Table 3) because it is one of two EPA-sanctioned color sets for the six official AQI categories. UV index colors are matched to it so the two read as one severity scale. Temperature has its own palette. Below are swatch colors used across the Weather, Air Quality, and UV cards.

### Temperature

| Range (°F) | Label | Color |
|---|---|---|
| < 32 | Freezing | `#8e44ad` 🟣 |
| 32–49 | Cold | `#3b82f6` 🔵 |
| 50–69 | Moderate | `#10b981` 🟢 |
| 70–78 | Temperate | `#d4a017` 🟡 |
| 79–89 | Hot | `#e67e22` 🟠 |
| 90–99 | Very Hot | `#c0392b` 🔴 |
| ≥ 100 | Extreme | `#ec4899` 🩷 |

### Air Quality Index (AQI)

EPA's [ColorVision Assist](https://document.airnow.gov/technical-assistance-document-for-the-reporting-of-daily-air-quailty.pdf)
palette is used in Wye Tide instead of the standard palette for better contrast on a dark theme. Breakpoints are the AQI's official definition and are not adjustable; see `DATA SOURCE COMPLIANCE` in `index.html`.

| AQI | Category | Color |
|---|---|---|
| 0–50 | Good | `#9eff91` 🟢 |
| 51–100 | Moderate | `#ffc905` 🟡 |
| 101–150 | Unhealthy for Sensitive Groups | `#ff8205` 🟠 |
| 151–200 | Unhealthy | `#f02200` 🔴 |
| 201–300 | Very Unhealthy | `#890997` 🟣 |
| 301+ | Hazardous | `#640015` 🟤 |

### UV Index

Matched to the first five stops of the AQI ColorVision Assist palette above, so
UV and AQI read as one severity scale. The AQI's "Hazardous" category is
intentionally unused here — UV has no tier equivalent to hazardous air.

| UV Index | Category | Color |
|---|---|---|
| 0–2 | Low | `#9eff91` 🟢 |
| 3–5 | Moderate | `#ffc905` 🟡 |
| 6–7 | High | `#ff8205` 🟠 |
| 8–10 | Very High | `#f02200` 🔴 |
| 11+ | Extreme | `#890997` 🟣 |

## Licensing

The [MIT license](LICENSE) covers the source code of this repository only. It does not, and cannot, license:

- **The data** fetched at runtime. Each provider's terms govern. Open-Meteo's data stays CC&nbsp;BY&nbsp;4.0 no matter what this repo says.
- **Any AirNow API key.** A credential isn't a work to be licensed, and MIT grants everyone the right to "use, copy, modify, publish, distribute, and sublicense" the software without restriction — which is not a grant the key holder can make. That's why the key lives in `airnow-key.js`, carved out of the MIT grant, rather than in `index.html`. **If you fork Wye Tide, get your own free key**. The rate limit is enforced per key, so borrowing one breaks the dashboard for its owner.

## Credits

Wye Tide was created and is maintained by [Abby Walter](https://github.com/lawalter). Portions of this code were generated with AI assistance. Architecture, data-source selection, design decisions, and review are the author's. Compliance details are in [`DISCLAIMER.md`](DISCLAIMER.md).

Title font is set in [Fraunces](https://fonts.google.com/specimen/Fraunces) (OFL). The umbrella glyph comes from [Bootstrap Icons](https://icons.getbootstrap.com/) (MIT).
