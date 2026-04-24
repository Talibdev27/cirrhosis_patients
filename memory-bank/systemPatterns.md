# System Patterns

## Architecture Pattern
Tabular ML pipeline pattern:
1. Load `train.csv` and `test.csv`
2. Split features/target from train data
3. Apply preprocessing for numeric and categorical fields
4. Train one or more multi-class models
5. Validate with log loss
6. Generate test probabilities
7. Save submission CSV

## Modeling Pattern
- Baseline-first approach:
  - start with simple, reproducible baseline
  - track validation score
  - iteratively improve
- Recommended families for tabular multi-class:
  - gradient boosting (LightGBM/XGBoost/CatBoost if available)
  - tree ensembles
  - regularized linear baseline for reference

## Evaluation Pattern
- Use stratified validation when possible for class balance.
- Optimize strictly for multi-class log loss.
- Keep probability outputs calibrated and stable.

## Reproducibility Pattern
- Fix random seed values.
- Store model and preprocessing config used for each run.
- Save experiment notes with score, feature set, and model parameters.
