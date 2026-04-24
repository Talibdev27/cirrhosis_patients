# Cirrhosis Patient Survival Prediction

This repository contains a clean, reproducible workflow for the Mohirdev/Kaggle multiclass competition:

- Predict `Status_C`, `Status_CL`, `Status_D`
- Evaluate with multi-class log loss

## Project Files

- `siroz_finel_clean.ipynb` - final review-ready notebook (recommended to run)
- `notebook7cded29dbc.ipynb` - experimentation notebook
- `memory-bank/` - project context and progress documentation

## Dataset

Competition files:

- `train.csv`
- `test.csv`
- `sample_submission.csv`

The final notebook supports both:

- Kaggle path: `/kaggle/input/competitions/multiclassificationtask/`
- Local path: `data/` (put the three CSV files there)

## Modeling Workflow

The final notebook follows one linear pipeline:

1. Load and validate data paths
2. Keep target classes `C`, `CL`, `D`
3. Feature engineering for tabular medical features
4. Stratified 5-fold cross-validation
5. Train LightGBM, XGBoost, CatBoost
6. Blend model probabilities
7. Export `submission.csv`

## Output Format

Generated submission columns:

`id,Status_C,Status_CL,Status_D`

## How To Run

### On Kaggle

1. Upload/open `siroz_finel_clean.ipynb`
2. Run all cells
3. Download generated `submission.csv`
4. Submit to competition

### Locally

1. Create a `data/` folder in repo root
2. Add `train.csv`, `test.csv`, `sample_submission.csv`
3. Install required libraries (pandas, numpy, scikit-learn, lightgbm, xgboost, catboost)
4. Run `siroz_finel_clean.ipynb`

## Notes

- Main optimization target is multi-class log loss.
- Probabilities are normalized before saving submission.
- `memory-bank/` is kept updated to preserve project context between sessions.
