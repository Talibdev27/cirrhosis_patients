# Project Brief

## Project Name
Kasaalik Project - Cirrhosis Patient Survival Multi-class Prediction

## Goal
Build a practical machine learning workflow for the Mohirdev/Kaggle competition to predict patient status classes:
- `Status_C`
- `Status_CL`
- `Status_D`

The objective is to achieve strong leaderboard performance and document a reproducible data science pipeline for learning purposes.

## Competition Scope
- Platform: Kaggle (Mohirdev competition)
- Timeline: Nov 19, 2024 to Nov 18, 2025
- Dataset files:
  - `train.csv`
  - `test.csv`
  - `sample_submission.csv`
- Train target: `status` (categorical with 3 classes)
- Submission target columns:
  - `id`
  - `Status_C`
  - `Status_CL`
  - `Status_D`

## Success Criteria
- Primary metric improvement: lower multi-class logarithmic loss.
- Valid submission format with class probabilities per `id`.
- Reproducible training and inference workflow.
- Clear documentation in Memory Bank for future sessions.

## Constraints and Notes
- Probabilities are evaluated with multi-class log loss.
- Probabilities may be re-scaled by row in evaluation.
- Prediction values are clipped internally near 0 and 1.
- Learning-focused project: interpretability and experimentation are valuable.
