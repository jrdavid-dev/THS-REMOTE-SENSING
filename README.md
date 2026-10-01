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

All rasters are exported by Earth Engine on a fixed **EPSG:32651 (UTM 51N), 10 m** grid.

**Google Drive**

* `THS-SENTINEL2/`: one 5-band GeoTIFF per period (B3, B4, B5, B8, B11; raw DN), named `Sentinel2_CSPlus_<year>_<month>_<H1|H2>.tif`
* `THS-SENTINEL2-INDICES/`: one 3-band GeoTIFF per period (NDVI, NDRE, NDMI), named `S2_Indices_<year>_<month>_<H1|H2>.tif`. Masked pixels = `-9999` (NoData)
* `THS-SENTINEL2-FEATURES/`: one 192-band GeoTIFF per year, named `S2_FeatureStack_<year>.tif`
  * 24 semi-monthly periods × 8 features (B3, B4, B5, B8, B11, NDVI, NDRE, NDMI)
  * Band names: `<feature>_<month>_<H1|H2>`, e.g. `NDVI_03_H1`, ordered Jan H1 → Dec H2
  * Periods with no imagery or fully masked are kept as `-9999` (NoData), so every year has the same bands

**Local**

* `cloudscore_coverage_check.csv`: valid-pixel % and status (`good` / `partial` / `fully_masked` / `no_imagery`) per period

All outputs use the same scene filter (`CLOUDY_PIXEL_PERCENTAGE < 80`) and Cloud Score+ mask (`cs_cdf ≥ 0.6`), so the coverage check describes exactly the observations in the exported files.

Exports run in the background; track them at <https://code.earthengine.google.com/tasks>.
