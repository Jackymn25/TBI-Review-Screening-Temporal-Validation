# Released Model Policies

## Common policy contract

- Development period: 2017-2019
- Threshold-calibration period: 2020-2021
- Nominal calibration target: recall at least 0.95
- Decision rule: retain a record for simulated human review when its positive-class score is greater than or equal to the frozen threshold
- Random seed: 42
- Text representation for serialized-text policies: `[TITLE] {title} [ABSTRACT] {abstract}`
- Missing abstract representation: `[TITLE] {title} [ABSTRACT] [NO ABSTRACT]`

Text cleaning preserved Unicode, case, punctuation, numbers, and spelling; normalized surrounding and repeated whitespace; and did not apply stemming, lemmatization, or stop-word removal.

## Policy registry

| Policy | Model artifact | Score | Frozen threshold |
|---|---|---|---:|
| TF-IDF + logistic regression, Rank 1 | `tfidf-logistic-regression/rank-1/model.joblib` | Positive-class probability | 0.014407620283576934 |
| TF-IDF + logistic regression, Rank 2 | `tfidf-logistic-regression/rank-2/model.joblib` | Positive-class probability | 0.014388864006292685 |
| TF-IDF + logistic regression, Rank 3 | `tfidf-logistic-regression/rank-3/model.joblib` | Positive-class probability | 0.3112340697247115 |
| TF-IDF + linear SVM | `tfidf-linear-svm/model.joblib` | Decision function | -0.3181140754695802 |
| TF-IDF + multinomial Naive Bayes | `tfidf-naive-bayes/model.joblib` | Positive-class log probability | -8.500160148532075 |
| GTE 8192 + logistic regression | `encoder-logistic-regression/gte-8192/model.joblib` | Positive-class probability | 0.006067521371862778 |
| GTE 512 + logistic regression | `encoder-logistic-regression/gte-512/model.joblib` | Positive-class probability | 0.005400644067594143 |
| MedCPT 512 + logistic regression | `encoder-logistic-regression/medcpt-512/model.joblib` | Positive-class probability | 0.007062083699031333 |

The lexical `.joblib` files contain a dictionary with the fitted scikit-learn pipeline and frozen policy metadata. The encoder `.joblib` files contain the fitted logistic-regression classifier and frozen policy metadata. Use the threshold stored inside each bundle rather than a default 0.5 cutoff.

## Lexical policies

All lexical policies use an L2-normalized TF-IDF representation with sublinear term frequency and unigram features.

| Policy | `min_df` | Classifier settings |
|---|---:|---|
| Logistic regression, Rank 1 | 1 | `C=1`, no class weighting |
| Logistic regression, Rank 2 | 2 | `C=1`, no class weighting |
| Logistic regression, Rank 3 | 1 | `C=0.1`, balanced class weighting |
| Linear SVM | 1 | `C=0.01`, balanced class weighting |
| Multinomial Naive Bayes | 2 | `alpha=0.01` |

## Encoder policies

Encoder embeddings used the CLS token representation followed by L2 normalization in float32. The fitted classifier was logistic regression with `C=10`, no class weighting, the `liblinear` solver, and `max_iter=5000`.

| Role | External checkpoint | Revision | Maximum length | Input mode |
|---|---|---|---:|---|
| GTE 8192 | `Alibaba-NLP/gte-modernbert-base` | `e7f32e3c00f91d699e8c43b53106206bcc72bb22` | 8,192 | Serialized marked title and abstract |
| GTE 512 | `Alibaba-NLP/gte-modernbert-base` | `e7f32e3c00f91d699e8c43b53106206bcc72bb22` | 512 | Serialized marked title and abstract |
| MedCPT 512 | `ncbi/MedCPT-Article-Encoder` | `d05a736da4bb84ee4057b7f7999485be6ed85465` | 512 | Tokenizer title/abstract pair |

The encoder checkpoint files are not included. The released encoder policy cannot score text until the exact external checkpoint is obtained and used to reproduce the corresponding embedding contract.

## Serialization environment

The released models were serialized with:

- Python 3.12.4
- NumPy 2.5.0
- SciPy 1.18.0
- scikit-learn 1.9.0
- joblib 1.5.3

Encoder embeddings were produced with PyTorch 2.11.0+cu128 and Transformers 5.12.1. Using materially different library versions may prevent loading or change numerical behavior.

## Limitations

- Models were trained and evaluated within one systematic review update.
- Thresholds are policy-specific and score magnitudes are not comparable across model families.
- These files are research artifacts, not autonomous screening tools.
- TF-IDF bundles contain a fitted vocabulary derived from bibliographic text, but no complete titles, abstracts, record identifiers, or row-level predictions are released.
- Verify SHA-256 checksums before loading any `.joblib` file.
