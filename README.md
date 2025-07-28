# PhD Project – Mapping and Biomass Estimation of the Invasive Species Leucaena leucocephala in the State of São Paulo: An Integrated Approach Using Optical-LiDAR Data and Deep Learning

This repository contains all the source code, workflows, and documentation associated with the PhD research project of Matheus Siqueira Barros, developed at ESALQ/USP. The project is part of the FAPESP Thematic Project **"LiDAR Technology for Forest Monitoring in São Paulo"**, and supervised by Prof. Dr. Matheus Pinheiro Ferreira.

---

## 1 · Project Overview

This research aims to develop an integrated approach using **high-resolution remote sensing data** (LiDAR and RGBNIR) combined with **deep learning** techniques to:

- Automatically detect individual tree crowns (ITCs),

- Classify the invasive species _Leucaena leucocephala_,

- Estimate its aboveground biomass,

- Map its spatial distribution throughout São Paulo state.

The methodology includes the fusion of surface normals and intensity metrics from airborne LiDAR with optical imagery through CNN architectures (ResUNet), following the framework proposed by Ferreira et al. (2024), with extensions for state-wide application.

---

## 2 · Folder Structure

```

phd-leucaena-mapping/

│

├── 01-data/

│   ├── raw/                 # Raw LiDAR point clouds, RGBNIR orthomosaics

│   ├── processed/           # Preprocessed rasters, metrics, masks

│   └── shapefiles/          # Study area boundaries, ground truth samples

│

├── 02-notebooks/

│   ├── 01-segmentation/     # SAM-GEO crown segmentation notebooks

│   ├── 02-lidar-metrics/    # LiDAR metrics extraction and raster conversion

│   ├── 03-training/         # Model training, patch generation, evaluation

│   └── 04-inference/        # Large-scale inference and post-processing

│

├── 03-models/               # Saved model checkpoints and configs

│

├── 04-results/              # Maps, figures, performance metrics

│

├── 05-docs/                 # Manuscripts, proposals, presentations

│

├── environment.yml          # Conda environment specification

├── .gitignore               # Files to ignore in version control

└── README.md                # Project documentation

```

---

## 3 · Key Features

- **Multisensor fusion**: combines structural LiDAR features and spectral data.

- **SAM-based segmentation**: automatic ITC extraction using Segment Anything Model.

- **CNN hybrid modeling**: optical + LiDAR feature fusion via dual ResUNet.

- **Biomass estimation**: ITC-level modeling using LiDAR metrics and TLS/inventory calibration.

- **Scalable application**: designed for statewide Leucaena mapping in São Paulo.

---

## 4 · Setup

```

git clone https://github.com/matheussiba/phd-leucaena-mapping.git

cd phd-leucaena-mapping

conda env create -f environment.yml

conda activate leucaena

```

---

## 5 · Tutorials (Coming Soon)

- How to run ITC segmentation with SAM

- How to preprocess LiDAR and generate rasters

- Training CNNs with optical and structural features

- Applying models at scale across São Paulo

- Biomass estimation using TLS-calibrated models

---

## 6 · License

This project is licensed under the [MIT License](https://opensource.org/licenses/MIT). See the `LICENSE` file for details.

---

## 7 · Author

**Matheus Siqueira Barros**

PhD Candidate in Forest Resources – ESALQ/USP

[GitHub](https://github.com/matheussiba) | [LinkedIn](https://www.linkedin.com/in/msbarrosgis/)

---

## 8 · Acknowledgements

This project is supported by:

- **ESALQ/USP** – Department of Forest Sciences

- **CMQ Lab**

- **CePE-Geo**

- **CCarbon**

- **Prof. Dr. Matheus Pinheiro Ferreira**

---
