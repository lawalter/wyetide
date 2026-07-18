# Disclaimer and Data Attribution

Wye Tide is a personal, non-commercial dashboard. It does not produce weather,
air quality, or tide data. It fetches data from public providers at page load
and arranges it on screen. **The providers are the authority for their data;
this page is not.**

Nothing here is an official source. For anything that matters — a health
decision, a safety decision, going out on the water — go to the original
source. Links are in the footer of the page and below.

## Not official, and not a substitute for the source

- **Air quality data are preliminary.** AirNow observations have not been fully
  verified or validated, are subject to change, and must not be used to support
  regulation, ascertain trends, or back decision-making. Validated data live in
  EPA's Air Quality System (AQS).
- **Weather alerts are shown as issued, but this page is not an alerting
  system.** It does not push, poll, or notify. It shows what NWS returned the
  moment you loaded it. Do not rely on it to learn that a warning exists.
- **Tide values are predictions, not observations.** They are the official NOAA
  tide predictions, but they are astronomical predictions. Actual water levels
  vary with wind, pressure, and rainfall.
- **The page does not auto-refresh.** Every number is as old as your last page
  load. The footer timestamp says when that was.

## Data sources and their terms

Each provider's terms govern its own data, independently of this repository's
license. They are summarized here; the authoritative versions are linked.

### EPA AirNow — air quality (AQI)

Air quality observations are courtesy of the U.S. Environmental Protection
Agency AirNow program and the **state, local, and tribal air quality agencies**
that report to it. Those agencies own the data and are the authority for it.

Data are displayed as received. AQI values, categories, and cautionary
statements are not reworded, rescaled, smoothed, or blended with other sources.
AQI breakpoints and category descriptors follow EPA's *Technical Assistance
Document for the Reporting of Daily Air Quality*.

Terms: [AirNow Data Exchange Guidelines](https://docs.airnowapi.org/)

### NOAA / National Weather Service — forecast, observations, alerts

Weather forecasts, current observations, and hazard alerts come from the
National Weather Service. NWS is the sole authority for watches, warnings, and
advisories. Alert headlines, descriptions, and instructions are rendered as
issued.

A U.S. Government work; in the public domain.
Source: [api.weather.gov](https://api.weather.gov)

### NOAA CO-OPS — tide predictions

Official NOS tide predictions from the Center for Operational Oceanographic
Products and Services.

A U.S. Government work; in the public domain.
Source: [tidesandcurrents.noaa.gov](https://tidesandcurrents.noaa.gov/)

### Open-Meteo — pollutant concentrations, UV index

Pollutant concentrations, UV index, and (when no AirNow key is configured) a
fallback AQI estimate come from Open-Meteo.

**Open-Meteo data is used under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/),
with modifications**: values are rounded, reduced to daily maxima, and used to
derive burn time.

Open-Meteo's AQI is modeled output from the CAMS atmospheric composition
forecast, on a grid of roughly 40 km. It is a simulation, not a measurement,
and it will disagree with AirNow — most sharply during smoke events, when a
model cell averages a plume across thousands of square kilometres and a monitor
underneath it does not. When the page is showing an Open-Meteo AQI, it says so.

The free Open-Meteo tier is for non-commercial use. Adding advertising or
subscriptions to this page would make it commercial and require a paid plan.

Terms: [open-meteo.com/en/terms](https://open-meteo.com/en/terms)

### sunrise-sunset.org — solar times

First light, sunrise, sunset, and last light are courtesy of
[sunrise-sunset.org](https://sunrise-sunset.org/).

### Fraunces — typeface

Set in [Fraunces](https://fonts.google.com/specimen/Fraunces), used under the
[SIL Open Font License 1.1](https://openfontlicense.org/).

## Licensing

The MIT license in [LICENSE](LICENSE) covers **the source code of this
repository only.** It does not, and cannot, license:

- **The data.** It is not this project's to license. Each provider's terms
  apply to you directly if you reuse this code. Open-Meteo data remains CC BY
  4.0 regardless of what LICENSE says, and its attribution requirements travel
  with it.
- **Any AirNow API key.** Keys live in `airnow-key.js`, which LICENSE carves
  out. A credential is not a work. If you fork this repository, **get your own
  key** — it is free, and the rate limit is enforced per key, so borrowing one
  breaks the dashboard for its owner.

## No warranty

This page is provided as is, with no warranty of any kind, express or implied,
and no guarantee of accuracy, completeness, timeliness, or availability. The
author is not liable for any decision made on the basis of what it displays.
Each upstream provider disclaims warranties on its own data as well; see their
terms above.

## Reporting a problem

If something here misrepresents your data, misattributes it, or fails to meet
your terms, please open an issue at
<https://github.com/lawalter/wyetide/issues>.

---

*Last reviewed: July 2026.*
