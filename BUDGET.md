# Budget Plan

**Target: under $250, high end $300** | galacticlight | November 2026

Prices checked November 10, 2026. US retail.

## Core Hardware

| Item | Est. Cost | Notes |
| --- | --- | --- |
| Raspberry Pi 4 Model B, 4GB | $100 | Official list price as of Nov 2026 (raised from $75 in Apr 2026 due to memory costs). Pi 5 4GB is $110 if you want newer. |
| SD card, 32GB+ | $8 | For OS + local data logging |
| PMS5003 PM2.5/PM10 sensor | $15 | Amazon single unit ~$10-30; buy the $10-15 bare sensor, skip the $34 breakout bundle |
| MQ-135 gas sensor (NH3/NOx/CO2/smoke) | $5 | ~$3-7 each; broad but cheap air quality proxy |
| MQ-7 CO sensor | $8 | SparkFun SEN-09403 at $7.88 |
| BME280 temp/humidity/pressure | $9 | Waveshare $8.99; adds barometric context for altitude correlation |
| 10,000 mAh USB-C PD power bank | $21 | Baseus PD 45W at $20.99 (Best Buy deal); powers Pi + sensors independently of drone battery |
| Jumper wires, breadboard, misc | $10 | Headers, resistors, small enclosure bits |

**Core subtotal: ~$176**

## Mount & Structure

| Item | Est. Cost | Notes |
| --- | --- | --- |
| 3D printed riser/arm (if you have a printer) | $2 | ~50-100g of PLA at ~$10-15/kg spool |
| 3D print service (if no printer) | $25-40 | Shapeways/local service for custom CG-balanced mount |
| Optional bamboo/hardwood accent frame | $15-30 | Ties into joinery aesthetic; only if you want it |

**Mount subtotal: $2 (DIY print) to $70 (service + wood)**

## Software & Data (essentially free)

| Item | Est. Cost | Notes |
| --- | --- | --- |
| Flask/FastAPI local server | $0 | Runs on the Pi or existing home machine |
| SQLite / lightweight TSDB | $0 | Local storage, no cloud fees |
| Open-Meteo weather API | $0 | Free tier covers hyperlocal forecasts |
| EPA AQI breakpoint math | $0 | Standard linear equations, open spec |

## Grand Totals

| Scenario | Total |
| --- | --- |
| Lean (own 3D printer, bare sensors, no wood) | **~$178** |
| Mid (print service for mount, still no wood) | **~$201-216** |
| High end (print service + bamboo frame + buffer) | **~$248-286** |

All scenarios land at or under the $250 target, with the high end brushing $300 only if you add contingency for a second sensor round or a sturdier carbon-tube mast instead of printed PLA.

## Cost-Saving Levers

- **Pi Zero 2 W instead of Pi 4:** saves ~$70 but tight on GPIO and USB; only worth it if payload weight is the binding constraint
- **Skip MQ-7, rely on MQ-135:** saves ~$8; CO detection gets less precise but still indicative
- **Use existing power bank:** if you already have a 10K+ mAh PD bank, drop that $21 line entirely
- **Harvest jumper wires/breadboard from other projects:** saves ~$10

## What This Budget Does NOT Include

- The drone itself (assumed existing)
- FAA Part 107 certification if flying commercially (~$175 exam + $175 cert)
- Certified reference-standard calibration service (DIY baseline against a consumer AQI station instead)
- Spare sensors for field failures

## Notes

- Raspberry Pi prices have risen six times since Oct 2025; the $100 for a 4GB Pi 4 is the current reality, not a deal. If a 2GB at $67.50 suffices for ingestion + caching, that trims $32.50.
- The PMS5003 is the single most research-validated sensor in the reference papers (TROPOS, Springer); don't cheap out here.
- Power bank should be PD-capable so the Pi can boot from it directly via USB-C.