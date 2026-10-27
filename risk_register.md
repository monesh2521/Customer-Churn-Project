# Risk Register: Customer Churn Prediction

| Risk | Why it matters | Mitigation / action |
|---|---|---|
| Small, unrepresentative sample | 12 rows cannot represent a broad customer population or support reliable conclusions. | Obtain a larger documented dataset; label current metrics exploratory only. |
| False positive | A customer may be incorrectly flagged as likely to leave. | Do not automate penalties or price changes; use only for optional, helpful outreach with human review. |
| False negative | A customer likely to leave may not be flagged. | Monitor recall and errors; combine model output with other appropriate feedback. |
| Data leakage | Features measured after churn can make test performance misleading. | Define the prediction date and confirm timestamps; exclude post-outcome data. |
| Privacy / re-identification | Customer IDs could be linked to external records. | Exclude IDs from modelling; restrict raw-data access and do not publish row-level data without permission. |
| Proxy bias | Plan, spending, and activity may correlate with customer circumstances. | Review feature necessity and performance across appropriate groups when data and permissions allow. |
| Unknown provenance / permission | The supplied file does not document source or licence. | Ask the academy/data owner to confirm source, consent, licence, and allowed use before sharing or deployment. |
| Overconfidence / misuse | A tiny-sample score may be mistaken for a reliable prediction. | Document limitations; require larger validation, monitoring, and human oversight before any real use. |
