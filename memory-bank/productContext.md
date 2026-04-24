# Product Context

## Why This Project Exists
This competition supports learners in data science by providing a realistic classification task with medical-style tabular data. It creates a platform for young specialists to develop practical modeling skills and demonstrate potential.

## Problem It Solves
- Converts raw structured patient features into actionable status probability predictions.
- Trains participants on end-to-end ML workflow:
  - data understanding
  - preprocessing
  - model training
  - validation
  - submission creation

## Intended User Experience
- Quick setup from provided CSV files.
- Straightforward experimentation with multiple models.
- Fast feedback from local validation and leaderboard scores.
- Clear submission generation that matches Kaggle format.

## Output Expectations
For each `id` in `test.csv`, the system outputs three probabilities:
- `Status_C`
- `Status_CL`
- `Status_D`

The output must preserve the required CSV header and row format.
