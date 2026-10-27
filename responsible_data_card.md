# Responsible Data Card

## Dataset purpose
This dataset may support an exploratory baseline model that estimates whether a customer is marked as churned (`churned`). It should only be used for learning and initial evaluation. It must not be used by itself to deny service, change prices, penalize customers, or make consequential decisions about an individual.

## Provenance and permission
The supplied file is named `customer-churn-training.csv`. The file itself does not identify its original creator, collection process, consent terms, licence, or permitted audience. These details are **unknown and must be confirmed with RabTech Academy or the dataset provider** before any external or production use. Customer IDs are present; avoid publishing raw row-level data publicly unless permission is confirmed.

## Population and representation
The file contains 12 rows and 7 columns. It contains 5 rows with `churned=1` and 7 with `churned=0`. Plan types are Basic (5), Standard (4), and Pro (3). The source does not explain the sampling method, time period, customer population, geography, or which groups are absent. With only 12 records, the sample is too small to establish that the data represents real customers or to assess fairness reliably.

## Features and target
- `customer_id`: customer identifier; exclude from model inputs because it is an identifier, not a useful generalizable predictor.
- `tenure_months`: customer tenure in months; presumed duration, confirm definition with provider.
- `support_tickets`: number of support tickets; the counting period is not specified.
- `monthly_spend_inr`: monthly spend in Indian rupees, based on the column name.
- `last_login_days`: number of days since last login, based on the column name; reference date is not specified.
- `plan_type`: plan category (Basic, Standard, Pro).
- `churned`: target label, with 1 interpreted as churn and 0 as no churn based on the dataset name/task context; confirm this coding with the provider.

Potential leakage: confirm that all feature values are measured before the churn decision/outcome. In particular, `last_login_days` must be measured at a clearly defined prediction date and must not include information recorded after churn. Plan type or spending may act as proxies for customer circumstances. No explicit sensitive attributes are listed, but absence of such columns does not prove the data is free from proxy bias.

## Quality checks
- Rows: 12; columns: 7.
- Missing values: none found in the supplied file.
- Exact duplicate rows: 0.
- Duplicate `customer_id` values: 0.
- Target counts: 7 non-churn (0), 5 churn (1), approximately 58.3% and 41.7%.
- Numeric ranges observed: `tenure_months` 1–30; `support_tickets` 0–5; `monthly_spend_inr` ₹499–₹1,499; `last_login_days` 1–30. These ranges are observations, not verified business rules.
- Split: use a fixed random seed and keep the test set separate from preprocessing/model fitting. The dataset is too small for reliable performance estimates; results are highly sensitive to which rows are held out.

## Risks and safeguards
- **False positives:** a customer is flagged as likely to churn but stays. Mitigation: treat the score as a prompt for optional, helpful outreach, not an automatic action.
- **False negatives:** a customer churns but is not flagged. Mitigation: monitor errors and do not rely only on model predictions.
- **Bias / representation:** the small, undocumented sample may not represent all customers. Mitigation: obtain a documented, larger, representative dataset and evaluate performance across appropriate groups where lawful and feasible.
- **Privacy / re-identification:** customer IDs may be linkable to people in another system. Mitigation: remove identifiers from modelling and public reports; restrict access to raw data.
- **Misuse / overconfidence:** tiny-sample metrics may look better or worse by chance. Mitigation: label results as preliminary and do not deploy without larger validation and human oversight.
- **Data leakage:** features may include information from after the outcome. Mitigation: define a prediction date and verify feature timestamps with the data owner.

## Intended evaluation
Before training, compare against a simple majority-class baseline and a Logistic Regression baseline in a scikit-learn preprocessing pipeline. Report accuracy, precision, recall, F1-score, confusion matrix, and (where meaningful) ROC-AUC. Inspect false positives and false negatives. Consider probability calibration only with a much larger dataset. Fairness evaluation is not reliable with 12 records; document this limitation rather than claiming the model is fair. Use a fixed random seed and keep preprocessing inside the training pipeline to avoid leakage.
