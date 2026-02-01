# Repository Structure Overview

- Our GitHub repository is structured to clearly separate data preparation, model training, balancing strategies, cross-validation, and result evaluation.
- Each notebook has a specific role in the workflow and builds on the outputs of the previous steps.

---

## Main notebooks

- **LoadingData.ipynb**
- **BalancingData.ipynb**
  - Only used to explore options
  - Random oversampling was chosen in the final approach
- **PersonalCrossVal.ipynb**
- **all_CV_results.ipynb**

---

## Intermediate outputs (saved to ensure reproducibility)

- **Encoded feature files**
  - `train_X_*.csv`
  - `train_X_*.npz`
  - `train_X_*.npy`

- **Label files**
  - `train_y_*.csv`
  - `test_y_*.csv`

- **Result files**
  - `genomic_ml_results_partial.pkl`

---

## LoadingData.ipynb – Data Loading & Preprocessing

- **Purpose**
  - This notebook handles all initial data preparation steps
  - Ensures that the dataset is clean, consistent, and ready for machine learning

- **Main steps**
  - Load the genomic variants dataset (`variants.csv`)
  - Remove samples with missing labels
  - Split the dataset into:
    - Features (`X`)
    - Labels (`y`) for each antibiotic (CIP, CTX, CTZ, GEN)
  - Perform a stratified train–test split to preserve class distributions
  - Apply three encoding strategies:
    - Label encoding
    - One-hot encoding
    - FCGR encoding
  - Save all processed train/test splits to disk

- **Output files**
  - `train_X_label.csv`, `test_X_label.csv`
  - `train_X_OneHot.npz`, `test_X_OneHot.npz`
  - `train_X_fcgr.npy`, `test_X_fcgr.npy`
  - `train_y_CIP.csv`, `train_y_CTX.csv`, `train_y_CTZ.csv`, `train_y_GEN.csv`

- These saved files are reused by all other notebooks to guarantee consistent inputs

---

## Functions

- **Main functions**
  - `run_model`
    - For running individual models
  - `cross_validate_model`
    - For cross-validation and result saving

- All other minor functions can be read and understood within the context and notebook they are used in
