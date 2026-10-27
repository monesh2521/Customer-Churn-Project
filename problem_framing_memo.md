# Problem-Framing Memo: Customer Churn Prediction

## Decision and purpose
Build an educational baseline that predicts the supplied `churned` label from customer attributes available before a defined prediction date. The possible business use is to help a team offer voluntary support or retention information to customers who may need it.

## What the model predicts
The supplied dataset has a `churned` column. For this project, interpret `1` as churn and `0` as no churn, but confirm this coding with the dataset provider before relying on it.

## Inputs
Candidate features are `tenure_months`, `support_tickets`, `monthly_spend_inr`, `last_login_days`, and `plan_type`. Exclude `customer_id` from model inputs. Verify feature definitions and timestamps with the data owner, especially whether all values were known before the churn outcome.

## Users and limits
The intended audience is a student/mentor reviewing a baseline ML workflow. Predictions are not suitable for production or high-impact decisions. Do not use the model to deny service, set prices, penalize customers, or automatically target people without review.

## Success measures
Compare a majority-class baseline with Logistic Regression. Report precision, recall, F1-score, accuracy, confusion matrix, and ROC-AUC if the test set contains both classes. Discuss false positives and false negatives. Since the dataset has only 12 rows, metrics are exploratory and cannot establish real-world performance.

## Assumptions and open questions
- What is the source, collection date, and licence/permission for the dataset?
- What precisely does `churned=1` mean, and over what period?
- When were features measured relative to churn?
- What population does the dataset represent?
- Are there missing groups or systematic sampling biases?

## Expected outcome
A reproducible notebook, a responsible data card, and a risk register documenting the baseline, limitations, and safeguards.
