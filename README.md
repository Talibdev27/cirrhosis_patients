# Cirrhosis Patient Survival Prediction

Multiclass probability model for the Mohirdev Kaggle competition [*Sirroz bemorlari omon qolish prognozini aniqlash*](https://www.kaggle.com/competitions/multiclassificationtask): predict whether a cirrhosis patient is alive (**C**), alive because of a liver transplant (**CL**), or dead (**D**) at the end of follow-up. Scored by **multiclass log loss**.

➡️ **[`cirrhosis_final.ipynb`](cirrhosis_final.ipynb)** is the full pipeline, committed with its outputs.

## Results

Stratified 5-fold cross-validation, scored on out-of-fold (OOF) predictions over 14,999 training rows. Lower is better.

| Model | OOF log loss | ± fold std |
|---|---:|---:|
| Class frequencies (no model) | 0.7235 | 0.0004 |
| Logistic regression | 0.4615 | 0.0124 |
| LightGBM | 0.3729 | 0.0094 |
| XGBoost | 0.3711 | 0.0097 |
| CatBoost | 0.3827 | 0.0086 |
| **Blend** (0.28 LGB · 0.67 XGB · 0.05 CAT) | **0.3706** | 0.0095 |

All three boosters are trained on the competition data plus the original clinical dataset (see Findings).
**Leaderboard (late submission, Oct 2026):** public **0.35629**, private **0.34867**. On the public leaderboard that would rank 2nd of 35 teams. It was submitted after the close, so it isn't officially ranked. The test score is better than the OOF score, so the CV estimate is, if anything, conservative.

## Findings

1. **Gradient boosting clearly beats the linear baseline.** Log loss drops from 0.461 to 0.371.
2. **Adding the real patient data helps.** The competition data is synthetic, generated from the 418-patient [Mayo Clinic PBC study](https://archive.ics.uci.edu/dataset/878/cirrhosis+patient+survival+prediction+dataset-1). Adding those real patients to every training fold (validation stays on competition rows only) improves all three boosters by 0.003–0.004, more than 2 standard errors each time.
3. **The published clinical score didn't help.** I added the Mayo risk score (Dickson et al., *Hepatology*, 1989), the standard survival model for this disease, as a feature. It failed the ablation, and so did the ratio features and the hand-made scores. The boosters already rebuild these combinations from the raw lab values, so the final model uses only the raw features.
4. **Class weighting hurts under log loss.** `class_weight='balanced'` makes LightGBM worse, from 0.376 to 0.401, because it nearly doubles the predicted probability of the rare CL class (0.037 vs a true share of 0.025).
5. **The blend adds little.** It improves on XGBoost alone by only 0.0005, because the three boosters make very similar errors.

**How decisions were made.** Every "keep it or not" choice (feature groups, the extra data) uses the same rule. All runs share the same folds, and a change is kept only if it lowers log loss by more than two standard errors of the paired per-fold difference. Early stopping uses an inner split of each training fold, never the validation fold. Blend weights are fitted by minimising OOF log loss.

**Limitations.** Hyperparameters are sensible defaults, not tuned. Results come from a single 5-fold split with one seed.

## Repository

| Path | Contents |
|---|---|
| [`cirrhosis_final.ipynb`](cirrhosis_final.ipynb) | Final pipeline: data checks, features and ablation, CV, original-data experiment, blend, submission |
| [`notebooks/exploration.ipynb`](notebooks/exploration.ipynb) | Early exploration and the first logistic regression baseline |
| [`CONTEXT.md`](CONTEXT.md) | Glossary of domain terms (Status classes, N_Days, Mayo risk score, …) |

<details>
<summary><b>How to run</b></summary>

**Kaggle:** open `cirrhosis_final.ipynb` in the competition, optionally attach a copy of the original dataset (`cirrhosis.csv`), and run all cells. Without it, the original-data experiment is skipped.

**Locally:** put `train.csv` and `test.csv` from the competition, plus `cirrhosis.csv` from the [UCI repository](https://archive.ics.uci.edu/dataset/878/cirrhosis+patient+survival+prediction+dataset-1), in a `data/` folder, then:

```bash
pip install pandas numpy scipy scikit-learn lightgbm xgboost catboost jupyter
jupyter nbconvert --to notebook --execute --inplace cirrhosis_final.ipynb
```

A full run takes about 5 minutes on a laptop CPU and writes `submission.csv` (`id,Status_C,Status_CL,Status_D`).

</details>
