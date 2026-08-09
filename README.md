# TBI Review Screening Temporal Validation

Public release artifacts from a retrospective temporal validation of machine-learning-assisted title-and-abstract screening within one traumatic brain injury systematic review update.

## setting & Unofficial Paper

This is a research project carried out in Kite Research Institute, UHN, Canada.

Authors: **Haozhe Huo; Urooba Shaikh; Cynthia Chui; Tatyana Mollayeva**

[Unofficial paper link](https://github.com/Jackymn25/TBI-Review-Screening-Temporal-Validation/blob/main/paper/TBI_screening_temporal_validation_content_only.md)

## Research question

The study examined whether screening policies developed on earlier records retained high recall when applied, without model or threshold changes, to later records from the same review update. It also quantified simulated human-review workload, temporal drift, and overlap among false negatives.

This is a within-review historical temporal validation. It does not establish generalizability to other reviews and does not support autonomous record exclusion.

## Study design

| Period | Role | Records | Reference-positive records |
|---|---|---:|---:|
| 2017-2019 | Model development | 6,463 | 75 |
| 2020-2021 | Threshold calibration | 5,597 | 58 |
| 2022-2024 | Historical temporal test | 7,203 | 62 |
| **Total** |  | **19,263** | **195** |

The threshold for each policy was calibrated to a nominal recall target of at least 0.95. The model and threshold were then frozen before historical-test evaluation.

## Released policies

Eight primary-data policies are included:

1. TF-IDF plus logistic regression, Rank 1 (prespecified primary policy)
2. TF-IDF plus logistic regression, Rank 2
3. TF-IDF plus logistic regression, Rank 3
4. TF-IDF plus linear support vector machine
5. TF-IDF plus multinomial Naive Bayes
6. GTE-ModernBERT at 8,192 tokens plus logistic regression
7. GTE-ModernBERT at 512 tokens plus logistic regression
8. MedCPT Article Encoder at 512 tokens plus logistic regression

The repository includes the fitted lexical pipelines and the fitted logistic-regression heads for the encoder policies. Third-party encoder checkpoints are not redistributed. Exact checkpoint identifiers and revisions are documented in [models/README.md](models/README.md).

## Main historical-test result

The prespecified primary policy retained 61 of 62 reference-positive records:

- Recall: **98.39%** (Wilson 95% CI, 91.41%-99.71%)
- False negatives: **1**
- Reference-negative workload retained for simulated review: **16.06%**
- Total workload retained for simulated review: **16.77%**
- Calibration-to-test recall drift: **+1.84 percentage points** (bootstrap 95% interval, -6.34 to +3.45)

Seven of eight policies met the nominal recall target by point estimate. Six unique reference-positive records were missed by at least one policy, but no record was missed by every policy. These findings are descriptive and do not establish screening safety.

## Repository contents

- [`models/`](models/): eight fitted primary policies, coefficient tables for encoder classifiers, and model documentation
- [`results/tables/`](results/tables/): aggregate policy metrics, bootstrap intervals, overlap sensitivity, truncation summary, and masked false-negative overlap
- [`results/figures/`](results/figures/): publication-ready aggregate figures
- [Unofficial paper link](https://github.com/Jackymn25/TBI-Review-Screening-Temporal-Validation/blob/main/paper/TBI_screening_temporal_validation_content_only.md): content-only scientific abstract in editable Markdown and PDF formats
- [`checksums/`](checksums/): SHA-256 checksums for released artifacts

## Deliberate exclusions

This repository does not contain:

- bibliographic records, titles, abstracts, DOI values, or record identifiers
- development, calibration, or test datasets
- record-level predictions, scores, embeddings, or tokenizer audits
- experiment configuration files, source code, internal logs, or the project knowledge base
- reviewer forms or internal false-negative annotations
- third-party encoder checkpoint files

## Model loading warning

The `.joblib` artifacts use Python pickle serialization. Never load a serialized model from an untrusted source. Verify the file against [`checksums/SHA256SUMS`](checksums/SHA256SUMS) before loading it.

## Interpretation boundary

The artifacts represent a frozen preliminary historical analysis. Future evaluation on a subsequent updated-search cohort, or any corrected full-paper analysis, should be released as a new version rather than silently replacing these results.

## License status

No general reuse license is granted for these repository artifacts at this time. Third-party checkpoint licenses and links are documented in [`LICENSES/README.md`](LICENSES/README.md).
