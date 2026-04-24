# Tech Context

## Current Stack (Expected)
- Language: Python
- Data processing: pandas, numpy
- Modeling: scikit-learn and/or gradient boosting libraries
- Validation metric: multi-class log loss
- Artifact format: CSV submission

## Data Files
- `train.csv` (contains features + `status`)
- `test.csv` (contains features without target)
- `sample_submission.csv` (submission template)

## Environment Notes
- Project currently starts with minimal structure.
- Memory Bank is initialized to preserve project context across sessions.

## Constraints
- Submission must match column names exactly:
  - `id,Status_C,Status_CL,Status_D`
- Every test row must have probability values for all three classes.
- Ensure no missing predictions in submission file.

## Suggested Next Technical Setup
- Create `notebooks/` for EDA and quick experiments.
- Create `src/` for reusable training/inference code.
- Add `requirements.txt` for dependency reproducibility.
