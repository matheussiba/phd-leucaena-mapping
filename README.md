# PhD Project — Mapping and Biomass Estimation of *Leucaena leucocephala* with Deep Learning

> **Matheus Siqueira Barros** — PhD Candidate in Forest Resources, ESALQ/USP
> Supervised by Prof. Dr. Matheus Pinheiro Ferreira

This repository is the central hub for the PhD research project on mapping and biomass estimation of the invasive species *Leucaena leucocephala* in the State of São Paulo (Brazil), using high-resolution remote sensing data (optical + LiDAR) and deep learning.

Part of the FAPESP Thematic Project **"LiDAR Technology for Forest Monitoring in São Paulo"**.

---

## Project Architecture

This project is organized as a set of independent, interconnected repositories:

```
phd-leucaena-mapping (this repo)
│   Project hub: documentation, notebooks, analysis
│
├── leucaena-earth-platform
│   Crowdmapping web platform (leucaena.earth)
│   Live at: https://map.leucaena.earth
│
└── leucaena-earth-segmentation
    Deep learning pipeline for binary segmentation
    Optical + LiDAR → ResUNet → Leucaena maps
```

### Repositories

| Repository | Description | Stack |
|:-----------|:------------|:------|
| **[phd-leucaena-mapping](https://github.com/matheussiba/phd-leucaena-mapping)** | Project hub — docs, notebooks, analysis | Jupyter, Python |
| **[leucaena-earth-platform](https://github.com/matheussiba/leucaena-earth-platform)** | Crowdmapping web platform ([leucaena.earth](https://leucaena.earth)) | Node.js, Express, SQLite, Google Maps |
| **[leucaena-earth-segmentation](https://github.com/matheussiba/leucaena-earth-segmentation)** | Binary segmentation pipeline (optical + LiDAR) | Python, PyTorch, GDAL |

### Data Flow

```
   Collaborators map leucaena canopy on the web platform
                        │
                        ▼
        ┌───────────────────────────────┐
        │   leucaena-earth-platform     │
        │   Polygon masks (GeoJSON)     │
        │   map.leucaena.earth          │
        └───────────────┬───────────────┘
                        │ export masks
                        ▼
        ┌───────────────────────────────┐
        │ leucaena-earth-segmentation   │
        │ Rasterize → Patch → Train    │
        │ ResUNet (optical + LiDAR)    │
        └───────────────┬───────────────┘
                        │ predictions
                        ▼
              Leucaena distribution maps
              Biomass estimation models
              State-wide application (SP → Brazil)
```

---

## Research Objectives

1. **Detect** individual tree crowns (ITCs) from aerial imagery
2. **Classify** the invasive species *Leucaena leucocephala* using deep learning
3. **Estimate** aboveground biomass using LiDAR metrics
4. **Map** spatial distribution across São Paulo state (and beyond)

---

## Methodology

- **Multisensor fusion**: RGBNIR aerial imagery (25 cm) + airborne LiDAR (4 pts/m²)
- **Crowdmapping**: collaborative mask creation via [leucaena.earth](https://leucaena.earth)
- **CNN architecture**: ResUNet with early/late/joint fusion variants
- **Biomass estimation**: ITC-level modeling with LiDAR-derived metrics and field calibration

Based on the framework by Ferreira et al. (2024), with extensions for:
- GeoJSON polygon masks (instead of raster labels)
- Binary segmentation (leucaena vs. background)
- State-wide scalable application

---

## Repository Structure

```
phd-leucaena-mapping/
├── README.md              # This file — project overview
├── LICENSE                # MIT License
├── notebooks/             # Jupyter analysis notebooks
│   ├── lidar-preprocessing/   # LiDAR → raster products
│   ├── analysis/              # Results analysis, figures
│   └── biomass/               # Biomass estimation models
├── docs/                  # Thesis text, papers, presentations
└── environment.yml        # Conda environment (future)
```

---

## Quick Start

### 1. Crowdmapping Platform

Visit [map.leucaena.earth](https://map.leucaena.earth) to contribute or explore mapped areas.

To run locally:
```bash
git clone https://github.com/matheussiba/leucaena-earth-platform.git
cd leucaena-earth-platform
npm install
node create-admin.js <username> <password>
npm start
```

### 2. Segmentation Pipeline

```bash
git clone https://github.com/matheussiba/leucaena-earth-segmentation.git
cd leucaena-earth-segmentation
conda create -n leucaena python=3.11 gdal -c conda-forge
conda activate leucaena
pip install -r requirements.txt

# Prepare data (rasterize masks + create patches)
python prep-data.py --optical data/optical.tif --lidar data/lidar.tif --masks data/masks.geojson

# Train
python train.py -e 1

# Predict & evaluate
python prediction.py -e 1
python evaluation.py -e 1
```

---

## Key Features

- **Open source**: all code, models, and workflows are publicly available
- **Crowdsourced mapping**: collaborative platform for large-scale data collection
- **Multisensor deep learning**: fuses optical and structural LiDAR features
- **End-to-end pipeline**: from crowdmapping to trained models to predictions
- **Scalable**: designed for São Paulo state, extensible to all of Brazil

---

## License

This project is licensed under the [MIT License](LICENSE).

---

## Author

**Matheus Siqueira Barros**
PhD Candidate in Forest Resources — ESALQ/USP

[GitHub](https://github.com/matheussiba) | [LinkedIn](https://www.linkedin.com/in/msbarrosgis/)

---

## Acknowledgements

- **ESALQ/USP** — Department of Forest Sciences
- **CMQ Lab**
- **CePE-Geo**
- **CCarbon**
- **Prof. Dr. Matheus Pinheiro Ferreira** — Supervisor
- **Prof. Dr. Felipe Ferrari** — [tree_fusion](https://github.com/felferrari/tree_fusion) original pipeline
- **FAPESP** — Thematic Project funding
