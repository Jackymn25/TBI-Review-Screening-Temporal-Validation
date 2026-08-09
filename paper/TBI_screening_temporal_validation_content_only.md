# Evaluating Machine Learning-Assisted Title and Abstract Screening to Support a Living Systematic Review on Cognitive Outcomes after Traumatic Brain Injury

**Haozhe Huo; Urooba Shaikh; Cynthia Chui; Tatyana Mollayeva**

## Research Objective

To evaluate the recall, simulated screening workload, and patterns of missed records of prespecified machine-learning-assisted title-and-abstract screening policies when tested on temporally held-out records from a completed traumatic brain injury systematic review update.

## Design

Retrospective, record-level temporal validation preceding prospective evaluation of a machine-learning-assisted screening workflow for a living systematic review (DOI: 10.1016/j.neubiorev.2019.01.011). Records were divided by publication year into development (2017-2019), threshold calibration (2020-2021), and final evaluation (2022-2024) sets. Records in the final set were not used for model development or threshold selection.

Eight prespecified policies represented three methodological groups: three logistic-regression configurations using term frequency-inverse document frequency (TF-IDF) examined configuration robustness; two alternative word-based classifiers examined classifier choice; and three pretrained text encoders examined context length and biomedical specialization. TF-IDF emphasizes informative words across titles and abstracts. The highest-ranked logistic-regression configuration was designated as the primary approach.

## Setting

KITE Research Institute, University Health Network, Ontario, Canada.

## Participants

The analysis included 19,263 bibliographic records: 6,463 for model development (2017-2019), 5,597 for threshold calibration (2020-2021), and 7,203 for temporally held-out testing (2022-2024). Of these, 195 reference-positive records were retained following title-and-abstract screening by two independent researchers.

## Intervention

Not applicable. The study evaluated a machine-learning-assisted screening workflow.

## Main Outcome Measures

Primary outcomes were recall with Wilson 95% confidence intervals (CI), false-negative count, proportions of reference-negative and total records retained for simulated human review, and calibration-to-test drift estimated from 10,000 bootstrap replicates per approach. False-negative overlap across approaches was exploratory.

## Results

The prespecified primary approach retained 61 of 62 reference-positive test records (one false negative; recall, 98.39%; 95% CI, 91.41%-99.71%) and 1,208 of 7,203 total records for simulated human review (16.77%), including 1,147 of 7,141 reference-negative records (16.06%). Recall drift was +1.84 percentage points (bootstrap 95% interval, -6.34 to +3.45), and reference-negative workload drift was -1.63 points (bootstrap 95% interval, -3.01 to -0.31).

Seven of eight approaches met the prespecified recall target. Naive Bayes missed five reference-positive records; the biomedical encoder retained all 62. Across machine-learning approaches, six unique reference-positive records were missed, but none by all approaches. Excluding records in rule-detected cross-period overlap groups did not change primary recall or false-negative results.

## Conclusions

Machine-learning-assisted screening may reduce simulated workload when combined with human oversight and safeguards for missed studies. The primary approach achieved high observed recall, and workload remained lower than during calibration. However, uncertainty in recall drift supports the need for continued evaluation in subsequent literature updates.

## Conflicts of Interest

None declared.
