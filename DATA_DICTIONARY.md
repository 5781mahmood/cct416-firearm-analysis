# Data dictionary

Source: [Toronto Police Service — Shooting and Firearm Discharges Open Data](https://data.torontopolice.on.ca/datasets/TorontoPS::shooting-and-firearm-discharges-open-data/about)

Local file: `shooting_firearm_discharges.csv`

## Fields used in this analysis

| Column | Type (approx.) | Meaning | How we use it |
|--------|----------------|---------|----------------|
| `OCC_YEAR` | integer | Year the incident occurred | Time trends; coerced numeric |
| `NEIGHBOURHOOD_158` | string | Neighbourhood name + code (158 geography) | Primary geography for rankings; rows labeled `NSA` are dropped |
| `EVENT_TYPE` | string | Incident category (e.g. Shooting, Firearm Discharge) | Event-type comparison |
| `INJURIES` | integer | Number of injuries recorded for the incident | Harm inputs; coerced numeric |
| `DEATH` | integer | Number of deaths recorded for the incident | Harm inputs; coerced numeric |

## Engineered field

| Column | Definition | Why |
|--------|------------|-----|
| `total_harm` | `INJURIES + DEATH` | Single severity score for ranking and correlation |

## Other columns in the file (available, not central to rankings)

| Column | Meaning |
|--------|---------|
| `OBJECTID` | Row identifier |
| `EVENT_UNIQUE_ID` | Unique event id from the source system |
| `OCC_DATE` | Occurrence datetime string |
| `OCC_MONTH`, `OCC_DOW`, `OCC_DOY`, `OCC_DAY`, `OCC_HOUR` | Calendar / time breakdowns |
| `OCC_TIME_RANGE` | Coarse time-of-day label (e.g. Night, Afternoon) |
| `DIVISION` | Police division |
| `HOOD_158` | Neighbourhood code (158) |
| `HOOD_140`, `NEIGHBOURHOOD_140` | Alternate 140-neighbourhood geography |
| `LONG_WGS84`, `LAT_WGS84`, `x`, `y` | Coordinates / projected location |

## Cleaning rules applied in the notebook

1. Coerce `OCC_YEAR`, `INJURIES`, `DEATH` to numeric (`errors="coerce"`).  
2. Drop rows missing year, injuries, death, or neighbourhood.  
3. Drop rows where `NEIGHBOURHOOD_158 == "NSA"`.  
4. Compute `total_harm`.

After cleaning in this project’s run: **6,759** incidents remaining from **6,829** raw rows (**70** removed).
