# CLAUDE.md — BIDS EEG Study Template

## Project Overview
BIDS-compliant EEG analysis pipeline template from the NeuroCognitive Imaging Lab (NCIL), Dalhousie University. All study-specific settings live in `config.json`.

## Directory Structure
```
BIDS/
├── config.json               # Central config — edit this for each study
├── sourcedata/               # Original raw data (write-protected, not shared publicly)
├── sub-???/                  # BIDS-compliant raw datasets per subject
├── derivatives/              # Processed outputs from each pipeline stage
├── stimuli/                  # Stimulus files
└── code/
    ├── 0_init/               # Initialize BIDS structure from config.json
    ├── 1_import_data/        # Convert raw EEG → BIDS format
    ├── 2_preprocessing_erp/  # Filter, ICA, epoch → derivatives/
    ├── 3_visualization_erp/  # ERP plots
    ├── 4_measurement_erp/    # Peak amplitude/latency extraction
    ├── 5_stats_erp/          # Linear mixed-effects models
    ├── 6_classification/     # SVM classification
    └── 7_stats_classification/
```

## Key Configuration (config.json)
- **EEG hardware**: Brain Products actiChamp, EasyCap M1 (easycap-M1 montage)
- **Channels**: 32 EEG + 2 EOG (HEOG, VEOG); ground at FCz; 32 non-cortical channels dropped during preprocessing
- **Raw format**: XDF (`.xdf`) → converted to BrainVision format for BIDS
- **Preprocessing filter**: 0.1–30 Hz (analysis), 0.5–30 Hz (ICA)
- **ICA**: Picard method, 25 components, z-threshold 2, random_state 42
- **Epochs**: −1 to +1s, no baseline at preprocessing; rereferenced to average
- **n_jobs**: 8 (parallel processing)

## ERP Components
The temaplte project shows how to measure two common ERP components, the N170 and N400. If you are interested in other components, you can change the settings in config.json to reflect the names, ROIs, and time windows relevant to your study.
| Component | Peak Lat | Window | ROI | Measure |
|-----------|----------|--------|-----|---------|
| N170 | 170ms | ±25ms | vertex (Cz, CP1, CP2, Pz) | neg peak |
| N400 | 300ms | ±100ms | vertex (Cz, CP1, CP2, Pz) | mean amplitude |

- Analysis window: −0.1 to 1.0s; baseline: −0.1 to 0s
- Outlier threshold: 2 SD; p-threshold: 0.05

## Tech Stack
- Python, Jupyter notebooks
- MNE, mne-bids, mne-bids-pipeline
- AutoReject (bad segment detection)
- Picard ICA
- SVM classifier (scikit-learn): 80/20 split, 10-fold CV

## Workflow
1. Edit `config.json` with study details
2. Run `code/0_init/0_init_BIDS_study.ipynb` to create BIDS structure
3. Copy raw data to `sourcedata/`, then run `code/1_import_data/` notebooks
4. Run `code/2_preprocessing_erp/1_preprocessing_batch.ipynb` (batch over all subjects)
5. Visualize → measure → stats → classification

## Notes for Claude
- Notebooks iterate over subjects found in the BIDS root directory
- Derivatives are saved per-stage under `derivatives/<stage_name>/`
- `config.json` fields propagate through all scripts — changes there affect everything downstream
- The template has `EDIT_ME` placeholders in config.json that should be replaced for real studies
