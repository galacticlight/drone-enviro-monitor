# Drone Environmental Monitor

**Project Proposal** | galacticlight | November 2026

## The Idea

Build a homegrown environmental monitoring system that layers custom sensing onto a consumer drone, capturing air quality and telemetry data in real time, aggregating it locally, and surfacing patterns over time through a personal dashboard.

The goal is not to replace the drone's built-in app. It's to add a layer the manufacturer never thought to build: environmental context tied to every flight.

## Why This, Why Now

- Research from TROPOS Leipzig (Nov 2026) showed particulate pollution at 100 meters can be 60% higher than ground-station readings, using inexpensive drone-mounted sensors with a dehumidifier and a rotor-wash-clearing intake duct.
- A Springer paper (Oct 2026) published a full open blueprint: Raspberry Pi 4 onboard brain, ~450g modular sensor suite (CO, NO2, O3, SO2, PM2.5), 1 Hz sampling, ThingSpeak cloud sync, web dashboard with geospatial overlays and EPA-standard AQI calculation.
- Commercial products exist (AIRINS Sniffer4D, Scentroid DR1000) but cost thousands and target industrial/regulatory use. Nothing consumer-grade does this well for a backyard flyer.
- This fits the pattern of other galacticlight projects: local-first tools with dashboards (Quantum Market Sentinel, workout tracker, Ledgerlight) built with Python/Flask or Astro/TS.

## System Architecture

### Onboard Payload
- **Brain:** Raspberry Pi 4 (Model B) or lighter Pi Zero 2 W for minimal weight
- **Sensors:** Modular suite measuring CO, NO2, O3, SO2, PM2.5 (PMS5003 or similar), plus temperature, humidity, barometric pressure
- **Sampling:** 1 Hz with onboard filtering and dynamic caching
- **Power:** Independent 10,000 mAh power bank so sensor runtime doesn't drain flight battery
- **Mount:** 3D-printed riser or carbon tube arm angling the intake forward and up, ~30 cm above rotor plane to avoid downwash contamination. Center-of-gravity placement critical. Modular so sensors swap without rebalancing.
- **Optional aesthetic:** bamboo or hardwood frame echoing Japanese joinery work

### Data Pipeline
- Telemetry (GPS lat/lon/alt, battery %, XYZ position, heading, speed) pulled from drone SDK or logged via companion computer
- Environmental readings timestamped and GPS-tagged
- Wireless sync to local home server (Flask/FastAPI) instead of cloud — privacy-first, consistent with other projects
- Store in SQLite or lightweight time-series DB for historical queries

### Dashboard (the creative layer)
- Interactive map overlaying flight paths with color-coded pollution heatmaps (green = good, purple = unhealthy, red = hazardous)
- Time-series graphs per pollutant with trend lines
- Flight journal: every session stitched into a cumulative map of the property, revealing drift patterns, repeated routes, wind-affected zones
- Cross-reference with Open-Meteo weather API and air quality APIs for context
- AQI calculated via EPA breakpoint equations
- CSV/PDF export for sharing

## Stretch Goals
- Geofence alerts when drone crosses user-defined boundaries
- Machine learning layer predicting pollution trends from historical + weather data
- Multi-drone fleet support
- Automated threshold alarms (e.g., PM2.5 spike triggers notification)

## Open Questions
- Which drone platform? DJI Matrice 300 RTK has 2.7 kg payload (proven with similar sensor loads); lighter consumer quads may need Pi Zero 2 W and minimal sensors
- FAA Part 107 considerations if flying commercially; recreational rules for backyard testing
- Sensor calibration against certified reference standards
- Rotor wash mitigation: ducted intake vs. mast height tradeoff for a small airframe

## References
- TROPOS/TU Delft Delhi particulate study (Nov 2026)
- Springer: UAV integrated IoT sensing platform for sustainable air quality monitoring (Oct 2026)
- AIRINS Sniffer4D Nano 2 Plus (commercial benchmark)
- Scentroid DR1000 Flying Laboratory (commercial benchmark)
- UAVChum (open-source drone + weather intel web app, Go)
- Seeed Studio Air Quality sensor + LinkIt ONE drone demo (YouTube)

## Status
- [ ] Repo initialized
- [ ] Hardware selection
- [ ] Sensor integration prototype
- [ ] Local server + ingestion endpoint
- [ ] Dashboard v1 (map + heatmap + time series)
- [ ] Flight journal / pattern analysis
- [ ] Calibration and field testing