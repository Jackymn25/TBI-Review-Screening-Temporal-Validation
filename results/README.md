# Aggregate Results

All files in this directory contain aggregate or masked results. No titles, abstracts, DOI values, source-row identifiers, record-level scores, or embeddings are included.

## Tables

- `primary_policy_metrics.csv`: absolute historical-test performance for the eight primary-data policies, including Wilson intervals and calibration-to-test drift
- `bootstrap_intervals.csv`: percentile intervals from 10,000 paired calibration/test bootstrap replicates per policy
- `strict_overlap_sensitivity.csv`: primary versus strict-overlap sensitivity results and the number of changed decisions among shared records
- `false_negative_overlap.csv`: masked overlap matrix for the six unique reference-positive records missed by at least one policy
- `truncation_summary.csv`: aggregate tokenizer-length and truncation counts for the encoder roles

## Figures

- `figure1_temporal_design.png`: development, threshold calibration, and historical temporal-test design
- `figure2_recall_intervals.png`: historical-test recall with Wilson 95% confidence intervals
- `figure3_recall_workload.png`: absolute recall and retained reference-negative workload
- `figure4_false_negative_overlap.png`: masked false-negative overlap across the eight frozen primary policies

## Metric definitions

- **Recall:** reference-positive records retained divided by all reference-positive records
- **False negatives:** reference-positive records falling below the frozen policy threshold
- **Retained-NO workload:** reference-negative records retained for simulated review divided by all reference-negative records
- **Total workload:** all records retained for simulated review divided by all records
- **Recall drift:** historical-test recall minus calibration recall
- **Workload drift:** historical-test retained-NO workload minus calibration retained-NO workload

The historical temporal test contained 7,203 records: 62 reference-positive and 7,141 reference-negative records. Bootstrap intervals reflect finite-sample uncertainty and should not be interpreted as proof of screening safety.
