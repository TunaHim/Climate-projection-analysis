# Climate Projection Analysis (2020–2039)

A collection of Jupyter notebooks that diagnose a high-resolution storm-resolving climate projection (2020–2039) on HEALPix grids. The notebooks cover ocean mixed-layer depth, sea-surface temperature, ocean vertical velocity, 2 m temperature and ITCZ/precipitation, cloud and precipitation tracking, atmospheric vertical cross-sections, and quick-look GRIB inspection.

This repository is intended as a **browseable Research Software Engineering portfolio** rather than a fully installable package. The original HPC data are not included, so the notebooks cannot be re-executed without local data copies.

## Repository contents

- — Analysis notebooks
  - `p2559_Omld.ipynb` — ocean mixed-layer depth analysis
  - `p2559_Osst.ipynb` — sea-surface temperature trends and maps
  - `p2559_Owo.ipynb` — ocean vertical velocity climatologies and trends
  - `p2559_t2m.ipynb` — 2 m temperature analysis and ERA5 comparison
  - `p2559_t2m_ITCZtpr.ipynb` — ITCZ and precipitation trends
  - `p2559_tctp.ipynb` — cloud cover and precipitation feature tracking
  - `p2559_tu_VP.ipynb` — zonal wind, temperature and vertical velocity cross-sections
- `environment.yml` — conda environment specification

All notebooks now begin with **"Why this notebook matters"** and **"Key techniques demonstrated"** sections. All outputs are embedded in the notebooks.

## Workflow

Each notebook follows the same structure:

1. **"Why this notebook matters"** and **"Key techniques demonstrated"** introductory cells, followed by a summary of purpose, required input data and expected outputs.
2. A configuration cell defining placeholder path variables (`PROJ2559_DIR`, `ERA5_DIR`, `FESOM_DATA_ROOT`, `GPFS_SCRATCH_DIR`).
3. Data loading and scientific analysis with `xarray`, `dask`, `healpy` and `cartopy`.
4. Plotting with `matplotlib` and `cmocean`.

Because the original output paths were large, outputs were cleared from `p2559_tctp.ipynb` and `p2559_Osst.ipynb` to keep the repository below GitHub’s file-size limits, then a curated set of representative figures was re-added to the notebooks themselves. 

## Example outputs

The notebooks retain their executed outputs, so representative figures can be viewed directly inside each notebook. Representative outputs include:

- SST trend map from `p2559_Osst.ipynb`
- ITCZ temperature and precipitation trend from `p2559_t2m_ITCZtpr.ipynb`
- Cloud cover and precipitation feature tracking from `p2559_tctp.ipynb`

## Required Python packages

The notebooks are written for Python 3.10 and use:

- `xarray`
- `dask`
- `numpy`
- `scipy`
- `pandas`
- `matplotlib`
- `cartopy`
- `cmocean`
- `healpy`
- `eccodes`
- `cfgrib`
- `seaborn`
- `tqdm`
- `xesmf`
- `scikit-image`
- `ipywidgets`

A conda environment file is provided in `environment.yml`.

## Expected input data

The notebooks read original DKRZ Levante HEALPix-grid NetCDF/GRIB output and ancillary data:

- `{PROJ2559_DIR}` — root of the projection experiment (2020–2039):
  - `ocean3d_dy/`, `ocean3d_mm/` — 3D ocean variables
  - `sfc_hr/tco2559_proj/` — hourly surface GRIB output
  - `sfc_hr/mn_means_sfc_*` — monthly surface means
  - `pl_dy/ana_var_*/` — 3D pressure-level diagnostics
  - `ocean2d_dy/`, `ocean3d_dy/` — 2D/3D ocean output
- `{ERA5_DIR}` — ERA5 reanalysis 2 m temperature (used in comparison sections)
- `{FESOM_DATA_ROOT}` — FESOM2 mesh diagnostic files (e.g. `MESHES_FESOM2.1/ng5/fesom.mesh.diag.nc`)
- `{GPFS_SCRATCH_DIR}` — optional archived GRIB root (only used in commented-out cells)

## Data sources and access

| Data | Format | Access |
|---|---|---|
| DestinE Climate DT storm-resolving projection (TCo2559, ~4–5 km), 2020–2039: ocean 2D/3D, hourly surface and pressure-level fields | GRIB and NetCDF on HEALPix grids | DKRZ Levante file system (DestinE project access); not public |
| ERA5 reanalysis (2 m temperature) | NetCDF | Copernicus Climate Data Store (C3S) |
| FESOM2 mesh files (NG5) | NetCDF | Same HPC system |

Data are opened lazily with xarray, Dask and cfgrib, so only the selected variables and periods are read into memory. Paths are placeholders, see *Expected input data*.

## Limitations

- The original HPC data are **not included** in this repository.
- Absolute HPC paths and usernames have been replaced with documented placeholder variables.
- Outputs from `p2559_tctp.ipynb` and `p2559_Osst.ipynb` were cleared because the original files were larger than GitHub’s 50 MB warning threshold; a curated set of representative figures has been re-added to each.
- The notebooks are provided for portfolio browsing; full re-execution requires the original data and a compatible HPC/conda environment.

## Notes

- The original climate datasets are not included because of their size and access restrictions.
- Absolute HPC paths have been replaced with placeholder variables for portability.
- These notebooks are provided as examples of scientific analysis workflows and are intended primarily as a software engineering and research portfolio.

## Licence

Code: MIT, see [LICENSE](LICENSE). Data: see *Data sources and access*; third-party data keep their own terms.
