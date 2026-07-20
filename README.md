# CAMP2Ex Ice Phase Analysis - Model Simulations

Analysis and visualization code for cloud microphysics simulations from the CAMP2Ex project, focusing on ice phase processes w/ a novel SIP (drop fragementation upon freezing) parameterization using the DHARMA LES w/ both bin and bulk microphysics schemes. This repository contains Jupyter notebooks for data processing and analysis of model simulations with outputs from DHARMA and compared against in stiu aircraft observations from the NASA P-3B and SPEC Learjet aircraft during the NASA CAMP2Ex campaign. 

## Quick Start

All analysis is performed in Jupyter notebooks. To run the analysis:

```bash
jupyter notebook
```

Then navigate to the desired notebook and execute cells in order.

### Dependencies

- Python 3.7+
- numpy
- matplotlib
- scipy
- xarray (for netCDF handling)
- netCDF4
- pickle
- Additional domain-specific analysis packages

Install dependencies via:
```bash
pip install numpy matplotlib scipy xarray netCDF4
```

## Data Requirements

The simulations use large netCDF files that contain model outputs. These files are **available upon request** and should be placed in an accessible directory referenced by the notebooks. 

Key data files needed:
- Simulation output netCDF files from DHARMA model runs
- Aircraft observations from CAMP2Ex field campaign

Intermediate processed data (`.npz` files) are included in this repository.

## Repository Structure

### Analysis Scripts (Figure Generation)

These notebooks generate the publication-quality figures for the paper:

| Notebook | Figures | Description | Key Dependencies |
|----------|---------|-------------|------------------|
| `plot_fig_6_bin_bulk_control_evolution.ipynb` | Figure 6 | Evolution of bin vs. bulk microphysics in control simulations | `cntl_bulk_ice_ABIFM_sounding_time_series.pkl`, `cntl_bin_ice_sounding_time_series.pkl` |
| `plot_fig_7_Ni_time_series.ipynb` | Figure 7 | Ice crystal number concentration time series | Multiple bin and bulk sounding pickle files (×15) |
| `plot_fig_8_3d_pdfs.ipynb` | Figure 8 | 3D probability distribution functions of cloud properties | `cntl_bulk_ice_ABIFM_test_sounding_time_series.pkl`, `cntl_bin_ice_sounding_time_series.pkl` |
| `plot_fig_9_domain_max_time_series.ipynb` | Figure 9 | Domain maximum time series of key variables | Multiple bin and bulk sounding pickle files (×6) |
| `plot_fig_10_11_evaluate_ABIFM_rates.ipynb` | Figures 10-11 | Evaluation of ABIFM ice multiplication rates | `dharma_3d*.nc` (raw model), `ABIFM_rates_all_sim_processed_data.pkl`, multiple `.npz` files |
| `plot_fig_12_13_16_PSDs.ipynb` | Figures 12, 13, 16 | Particle size distributions (PSD) analysis | (Self-contained visualization) |
| `plot_fig_14_15_noturb_plots.ipynb` | Figures 14-15 | No-turbulence simulation comparisons | `*_noturb_sounding_time_series.pkl`, `bin_noturb_histograms_log10_*.npz` |
| `plot_fig_D1_HM_plots.ipynb` | Figure D1 | Appendix: Histogram and distribution plots | Multiple bin and bulk sounding pickle files (×12), `bin_noturb_histograms_log10_*.npz` |

### Processing Scripts

Scripts for generating intermediate data products from raw model output:

- **`stitch_files_bin_ice.ipynb`** - Combines bin microphysics ice output files; Primary processing script for bin scheme data
- **`stitch_files_bulk_ice.ipynb`** - Combines bulk microphysics ice output files; Primary processing script for bulk scheme data
- **`stitch_files_bin_ice_tmp*.ipynb`** - Temporary/variant versions of bin file processing

### Analysis/Exploration Scripts

- **`compute_bin_CP_psds.ipynb`** - Computes cloud probe particle size distributions for bin microphysics
- **`compute_bin_CP_psds_with_1degC.ipynb`** - Variant with 1°C temperature resolution
- **`compute_bulk_CP_psds.ipynb`** - Computes cloud probe PSDs for bulk microphysics
- **`calc_psd_params.ipynb`** - Calculates PSD parameters (effective radius, etc.)
- **`make_bin_sounding_scalar_dictionaries.ipynb`** - Creates atmospheric sounding profiles for bin scheme
- **`make_bulk_sounding_scalar_dictionaries.ipynb`** - Creates atmospheric sounding profiles for bulk scheme
- **`explore_dharma_ice.ipynb`** - Exploratory analysis of ice phase properties
- **`explore_dharma_bin_ice.ipynb`** - Exploratory analysis of bin scheme ice properties
- **`construct_learjet_cloud_passes_manual.ipynb`** - Constructs cloud pass segments from Learjet observations
- **`construct_p3_cloud_passes_manual.ipynb`** - Constructs cloud pass segments from P3 observations
- **`plot_all_psds.ipynb`** - Overview of all PSD comparisons
- **`plot_bin_Nc_time_series.ipynb`** - Time series of cloud droplet number concentrations

### Intermediate Data Products

The following `.npz` (NumPy) files contain processed data used by the analysis scripts:

- **`joint_histograms.npz`** - Joint distributions of analyzed variables
- **`joint_histograms_ber_mmds.npz`** - Histograms with observed data distributions
- **`joint_histograms_mass_ratio.npz`** - Histograms of mass ratios
- **`joint_histograms_ni_abifmrates.npz`** - Ice number and ABIFM rates
- **`summary_histograms.npz`** - Summary statistics histograms
- **`summary_histograms_with_NcNr.npz`** - Summary histograms with cloud/rain droplet concentrations
- **`summary_histograms_with_NcNr_log10.npz`** - Log-scale summary histograms
- **`bin_noturb_histograms_log10.npz`** - No-turbulence bin scheme histograms
- **`bin_noturb_histograms_log10_cld.npz`** - Cloud-only no-turbulence histograms
- **`bin_noturb_histograms_log10_updraft.npz`** - Updraft regions, no-turbulence histograms

## File Dependencies for Figure Scripts

Each figure generation notebook has specific data dependencies. Below is a detailed breakdown:

### Intermediate Data Files (`.npz` - Included in Repository)

These are used directly by multiple figure scripts:

- `summary_histograms_with_NcNr_log10.npz` - Used by `plot_fig_10_11_evaluate_ABIFM_rates.ipynb`
- `joint_histograms_ber_mmds.npz` - Used by `plot_fig_10_11_evaluate_ABIFM_rates.ipynb`
- `joint_histograms_ni_abifmrates.npz` - Used by `plot_fig_10_11_evaluate_ABIFM_rates.ipynb`
- `joint_histograms.npz` - Used by `plot_fig_10_11_evaluate_ABIFM_rates.ipynb`
- `joint_histograms_mass_ratio.npz` - Used by `plot_fig_10_11_evaluate_ABIFM_rates.ipynb`
- `summary_histograms_with_NcNr.npz` - Used by `plot_fig_10_11_evaluate_ABIFM_rates.ipynb`
- `summary_histograms.npz` - Used by `plot_fig_10_11_evaluate_ABIFM_rates.ipynb`
- `bin_noturb_histograms_log10_cld.npz` - Used by `plot_fig_14_15_noturb_plots.ipynb`, `plot_fig_D1_HM_plots.ipynb`
- `bin_noturb_histograms_log10_updraft.npz` - Used by `plot_fig_14_15_noturb_plots.ipynb`, `plot_fig_D1_HM_plots.ipynb`

### Intermediate Data Files (`.pkl` - Generated by Processing Scripts)

These Python pickle files contain processed sounding time series data and must be generated by running the processing scripts first:

**Generated by `make_bin_sounding_scalar_dictionaries.ipynb`:**
- `cntl_bin_ice_sounding_time_series.pkl` - Used by Figures 6, 7, 8, 9, D1
- `sip_bin_ice_sounding_time_series.pkl` - Used by Figures 7, 9, D1
- `cntl_bin_ice_noturb_sounding_time_series.pkl` - Used by Figures 7, 14-15
- `sip_bin_ice_noturb_sounding_time_series.pkl` - Used by Figures 14-15
- `cntl_bin_ice_hm_sounding_time_series.pkl` - Used by Figure D1
- `sip_bin_ice_hm_sounding_time_series.pkl` - Used by Figure D1
- `sip_10x_bin_ice_sounding_time_series.pkl` - Used by Figures 7, 9, D1
- `sip_10x_bin_ice_noturb_sounding_time_series.pkl` - Used by Figures 7, 14-15
- `sip_10x_bin_ice_hm_sounding_time_series.pkl` - Used by Figure D1

**Generated by `make_bulk_sounding_scalar_dictionaries.ipynb`:**
- `cntl_bulk_ice_ABIFM_sounding_time_series.pkl` - Used by Figures 6, 7, 9, 8, D1
- `cntl_bulk_ice_ABIFM_hm_sounding_time_series.pkl` - Used by Figures 7, D1
- `cntl_bulk_ice_ABIFM_test_sounding_time_series.pkl` - Used by Figure 8
- `sip_bulk_ice_ABIFM_sounding_time_series.pkl` - Used by Figures 7, 9, D1
- `sip_bulk_ice_ABIFM_hm_sounding_time_series.pkl` - Used by Figures 7, D1
- `sip_10x_bulk_ice_ABIFM_sounding_time_series.pkl` - Used by Figures 7, 9, D1
- `sip_10x_bulk_ice_ABIFM_hm_sounding_time_series.pkl` - Used by Figure D1

**Generated by external processing (not included):**
- `ABIFM_rates_all_sim_processed_data.pkl` - Used by `plot_fig_10_11_evaluate_ABIFM_rates.ipynb`

### Raw Model Output Files (`.nc` - Available Upon Request)

Raw DHARMA simulation output files in NetCDF format are **not included in this repository**. These large files are referenced by the processing scripts:

- `dharma_3d*.nc` - DHARMA 3D model output fields (referenced by `plot_fig_10_11_evaluate_ABIFM_rates.ipynb`)

These files are available upon request from the authors. Contact for access to full simulation archives.

### Aircraft Observation Data

Aircraft data from the NASA CAMP2Ex campaign (P-3B and SPEC Learjet observations) are referenced and integrated into derived products (joint histograms, etc.). The full datasets are publicly available at:

**NASA CAMP2Ex Aircraft Data Archive:**
- [https://www-air.larc.nasa.gov/cgi-bin/ArcView/camp2ex](https://www-air.larc.nasa.gov/cgi-bin/ArcView/camp2ex)

## Workflow

### Typical Analysis Workflow

1. **Data Preparation** (if running from raw model output):
   - Run `stitch_files_bin_ice.ipynb` or `stitch_files_bulk_ice.ipynb` to process model output
   - Run sounding dictionary creation notebooks
   - Run PSD calculation notebooks

2. **Intermediate Analysis**:
   - Run exploratory notebooks like `explore_dharma_ice.ipynb`
   - Generate cloud pass datasets

3. **Publication Figures**:
   - Run `plot_fig_*.ipynb` notebooks to generate paper figures
   - Figures are saved to local output directories

### Reproducing Paper Figures

To reproduce the paper figures, ensure that:

1. Intermediate `.npz` data files are present (included in repo)
2. Required packages are installed
3. Run each `plot_fig_*.ipynb` notebook in any order

## Notes

- **Large Data Dependencies**: Raw model output netCDF files are not included in this repository due to size constraints. Contact the authors for access to simulation outputs.
- **Aircraft Data**: CAMP2Ex field campaign observations are included implicitly through derived products (joint histograms, etc.)
- **Notebook Execution**: Notebooks are designed to be run sequentially within themselves but can generally be run in any order if intermediate data is available.
- **Reproducibility**: Notebooks include inline comments explaining analysis steps and assumptions.

## Contact

For questions about the analysis or to request simulation output files, please contact the repository maintainer.

## Cite

If you use code or data from this repository, please cite the associated publication.
