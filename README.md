# README

This Repository contains files relative to the collaboration between Trangh Anh Nghiem and the Gozzi Lab for the analysis of parcel based functional connectivity (FC) and structural connectivity (SC) in parcels defined from the Allen Brain Atlas (ABA) ontology. 

It is linked to a dataset repository named `2026-07-17_Trang-Anh-Nghiem` described below.

This repository is mainly composed of oe notebook `2026-07-17_analysis.ipynb` used for both the extraction of parcel timeseries from 4D BOLD timeseries and generation of associated FC matrices (for reproducing the study with ana alternative parcellation) and examples of loading of the main files of interest as well as example of low level analysis. Most functionalities require the entire dataset, but all analyses can be run independently and are based on:

- `Param/connectome/00_full-SC-matrix_ncd.h5` the default SC connectome computed as explained below
- `1_data/02_FC-matrices/` which contains individual FC matrices in the fisher space (Pearson correlation values after applytin the Fisher transform *i.e.* arctanh)


# Dataset

It consists on 10 preprocessed BOLD timeseries of awake mice brains from [Gutierrez Barragan](https://www.sciencedirect.com/science/article/pii/S0960982221016912?via%3Dihub) as well as all parameter files to extract timeseries from a parcellation derived from the ABA ontology as well as scripts and data allowing to generate the associated structural connectome from ABA mouse brain tractography dataset [Oh et al. 2014](https://www.nature.com/articles/nature13186).

It contains three main folder:

- `1_data` preprocessed data 4D BOLD timeseries and derivatives to generate FC matrices
- `2_SC` contains scripts and data to generate the associated SC matrix
- `Params` contains multiple parameter files in the custom space of the Gozzi Lab *i.e* `chd8` space

The reference parcellation used for this study is `N53` which contains 106 unilateral parcels respectively left and right hemisphere associated to 53 acronyms in the ABA ontology (see below). All scripts have been designed to work with any other parcellation derived from the ABA ontology.

## `1_data`

Contains 3 subfolders:

- `00_bold-smoothed` contains the preprocessed 4D timeseries of 10 awake mice
- `01_bold-parcellated` contains timeseries extracted from `0_bold-smoothed` with `N53` parcellation
- `02_FC-matrices` contains the FC matrices computed from the timeseries contained in `01_bold-parcellated`

## `2_SC`

Contains a standalone repository to extract parcel based structural connectome as described in [Oh et al. 2014](https://www.nature.com/articles/nature13186).

It contains mainly one `python` script `generate_structural_connectivity_matrix_from_allen_parcels.py` and associated files to download the connectome from a list of regions based on their acronym in the ABA ontology. The use of the script is detailed in a sidecar `README.md` file.

**N.B.** This script requires a specific environment with `Python 3.6` to work correctly due to low maintainance of abagen API.

## `Params`

Contains all the required files to perform the generation and analysis of FC and SC matrices:
- `connectome` contains the SC matrix as computed with `2_SC` repository
- `parcellation` contains the files (labelled image as `.nii` file and sidecar metadata in `.csv` file) to characterise the parcels used for this analysis
- `templates` define the space (template and mask) used for this analysis: the default `chd8` space for `EPI` BOLD images from the Gozzi Lab

# List of parcels

```python
parcellation_ids = ['FRP', 'MOp', 'MOs', 'SSp-n', 'SSp-bfd', 'SSp-ll', 'SSp-m', 'SSp-ul', 'SSp-tr', 'SSp-un', 'SSs', 'GU', 'VISC', 'AUD', 'VIS', 'ACA', 'PL', 'ILA', 'ORB', 'AI', 'RSP', 'PTLp', 'TEa', 'PERI', 'ECT', 'OLF', 'CA', 'DG', 'ENT', 'SUB', 'PRE', 'POST', 'CTXsp', 'STRd', 'STRv', 'LSX', 'sAMY', 'PALd', 'PALv', 'PALm', 'PALc', 'DORsm', 'DORpm', 'LZ', 'MEZ', 'SCs', 'SNr', 'VTA', 'MRN', 'SCm', 'PAG', 'PRT', 'RAmb']
```
