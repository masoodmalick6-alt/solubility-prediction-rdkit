# Solubility Prediction with RDKit and Random Forest
### Rebuilding Palmer et al. (2007) in Python

**Author:** Masood Ur Rehman — MSc Drug Discovery and Development, Uppsala University

## What this project does
Predicts aqueous solubility (**logS**) of molecules from their structure. It rebuilds, from scratch and with open tools, the study by Palmer et al., *"Random Forest Models To Predict Aqueous Solubility"* (J. Chem. Inf. Model. 2007) — a paper I first met as a peer-review assignment in my Pharmaceutical Bioinformatics course.

## Dataset
- **ESOL** (Delaney) dataset: 1,128 compounds with measured log solubility
- Input: SMILES strings; target: measured logS

## Method
1. Compute 8 molecular descriptors from SMILES with **RDKit**: MolWt, LogP, TPSA, rotatable bonds, H-bond donors/acceptors, ring count, heavy atoms
2. Stratified-style 70/30 train–test split (`random_state=42`)
3. Train **Random Forest** regression (300 trees) and **Linear Regression** baseline in scikit-learn
4. Evaluate with R² and RMSE; 5-fold cross-validation; descriptor importance analysis

## Results
| Model | R² (test) | RMSE (test) |
|---|---|---|
| Linear Regression | 0.779 | 1.005 |
| Random Forest | 0.882 | 0.732 |

- Random Forest 5-fold cross-validation: **R² 0.887**
- Palmer et al. reported RF test R² ≈ 0.89, RMSE ≈ 0.69 on their dataset — this rebuild lands close.
- **LogP dominates** descriptor importance (0.81), matching the paper's finding that lipophilicity drives solubility prediction.

## Files
- `solubility_project_ALL_STAGES.ipynb` — the full notebook (Google Colab)
- `solubility_model_comparison.csv` — model results

## Tools
Python · RDKit · pandas · scikit-learn · Google Colab

*Educational project. Not a chemical safety assessment.*
