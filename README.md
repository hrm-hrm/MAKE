## Requirements
- Python 3.8+
- PyTorch 1.13+
- pandas, numpy, scikit-learn

## Data Preparation

All data used in this study come from The Cancer Genome Atlas (TCGA) and are publicly available through the NCI Genomic Data Commons (https://portal.gdc.cancer.gov). We do not redistribute them in this repository. Specifically, we use:

- TCGA-BRCA (921 whole slide images with paired genomic profiles) and TCGA-GBM (176 patients).
- Whole slide images, tiled into 256 x 256 patches at 20x magnification following the CLAM pipeline and encoded into 768-D feature bags with the pre-trained CTransPath encoder.
- Somatic mutation profiles (MAF files), from which we derive the variant allele frequency (VAF) of driver mutations, the 96-channel single base substitution (SBS96) profile, and tumor mutational burden (TMB).
- DNA methylation profiles, used only to construct the High/Low methylation targets and the continuous epigenetic signature (PC1). The targets are fitted on the training split of each fold only.

To verify that the code runs without downloading TCGA data, generate a dummy dataset and place it in the `./data/` directory:

    python generate_dummy_data.py

## Usage

### 1. Training
To train the MAKE model using 5-fold cross-validation, run:
```bash
python train.py --fold 0 --use_kan 1 --w_pc1 0.1

### 2. Testing

    python test.py 
