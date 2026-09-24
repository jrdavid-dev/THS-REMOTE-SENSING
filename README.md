# Sentinel-2 Cloud-Free Composite Export (Paoay, Atok, Benguet)

A Jupyter notebook that uses Google Earth Engine to build half-month, cloud-masked Sentinel-2 median composites (2019–2023) for the Paoay study area and export them to Google Drive as GeoTIFFs. It also saves a CSV report of clear-sky coverage per period.

## Setup

**Requirements:** Python 3.12, a Google account with [Earth Engine access](https://code.earthengine.google.com/register), and a Google Cloud project registered for Earth Engine.

```bash
# 1. Create and activate a virtual environment
python -m venv venv
venv\Scripts\activate          # Windows
source venv/bin/activate       # macOS / Linux

# 2. Install dependencies
pip install -r requirements.txt
```

Then open `01_notebook_SENTINEL2_QUERY.ipynb` and run

## Output

- **Google Drive** (`THS-SENTINEL2/`): one GeoTIFF per period, named `Sentinel2_CSPlus_<year>_<month>_<H1|H2>.tif`
- **Local:** `cloudscore_coverage_check.csv`

Exports run in the background; track them at <https://code.earthengine.google.com/tasks>.
