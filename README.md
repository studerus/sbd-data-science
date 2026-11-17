# Sustainable Business Development: Data Science

Teaching data for the Data Science course in the Master of Sustainable Business Development, autumn semester 2026, taught by Erich Studerus.

## Seattle buildings: fixed 2024 teaching dataset

[`seattle_buildings_2024.csv`](seattle_buildings_2024.csv) contains **3,243 buildings**. One row represents one selected Seattle building in reporting year 2024.

### Use in Google Colab

No manual CSV upload or GitHub account is required to read this public file:

```python
import pandas as pd

url = "https://raw.githubusercontent.com/studerus/sbd-data-science/f54939bbee9d22fee0d8401e57a2140ddfed00b3/seattle_buildings_2024.csv"
df = pd.read_csv(url, index_col='Building_ID')
```

The URL selects a fixed commit so that the course notebooks keep using the same data if this repository changes.

### Columns

| Column | Meaning | Unit |
|---|---|---|
| `Building_ID` | City's OSEBuildingID, retained for traceability; not a predictor | Identifier |
| `Building_Type` | Primary property use (EPAPropertyType) | Category |
| `Floor_Area_m2` | Building floor area excluding parking (PropertyGFABuildings) | m² |
| `Parking_Area_m2` | Parking area (PropertyGFAParking) | m² |
| `Floors` | Occupiable floors at or above ground | Count |
| `Building_Age` | 2024 minus construction year | Years |
| `Energy_Use_MWh` | Annual total on-site energy use from all energy sources (SiteEnergyUse(kBtu)) | MWh/year |

The target is **total annual energy consumption**, not heating alone, electricity alone, energy per square metre, or emissions.

### Source and rights

Publisher: **City of Seattle, Office of Sustainability and Environment**.

- [Building Energy Benchmarking Data](https://data.seattle.gov/Built-Environment/Building-Energy-Benchmarking-Data-2015-Present/teqw-tu6e)
- [Official dataset metadata](https://cos-data.seattle.gov/api/views/teqw-tu6e.json)
- [Official CSV export](https://cos-data.seattle.gov/api/v3/views/teqw-tu6e/export.csv?accessType=DOWNLOAD)

The source metadata downloaded on **17 November 2026** identifies the data licence as **Public Domain**. This repository provides a prepared teaching subset of that source, not an official City of Seattle publication. The live source may change; the course file is a fixed snapshot.

### Preparation

Only reporting year 2024 was retained. Sequential exclusions from 3,712 source records were:

| Step | Excluded records |
|---|---:|
| Reporting status not Compliant / No Issue | 137 |
| Number of buildings not equal to one | 221 |
| Missing or non-positive annual energy use | 106 |
| Fewer than one above-ground floor | 5 |
| **Retained** | **3,243** |

Additional checks require positive building area, nonnegative parking area, a construction year between 1800 and 2024, a known primary property type, and no demolition flag. These checks excluded no additional records after the earlier steps.

Unit conversions: square feet × 0.09290304 → m²; kBtu × 0.0002930710701722222 → MWh. Age = 2024 − construction year.

No target-based upper cutoff, percentile trimming, imputation, scaling or model-dependent row selection was applied. Large consumers remain in the file. Each building occurs once. Fuel components, energy intensities, emissions and ENERGY STAR scores are excluded from the predictor table because they contain measured energy information unavailable in the teaching scenario.

### Scope

The benchmarking programme mainly covers large non-residential and multifamily properties. This complete-data subset is not representative of all Seattle homes. Reporting flags do not guarantee error-free measurements. Prediction results for these buildings do not establish future-year performance, accuracy in other countries, or causal effects of renovations.

### Integrity

CSV size: 234,838 bytes. SHA-256:

`272e10f0140ec20dfe57a6b2742f33bfc7c15b67472158781263df3edf8732a6`
