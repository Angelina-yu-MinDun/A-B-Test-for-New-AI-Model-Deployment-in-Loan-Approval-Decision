# A/B Test for New AI Model Deployment in Loan Approval Decisions

This project evaluates whether deploying a new AI model improves loan approval decisions compared with a legacy model. The analysis focuses on loan-officer-level outcomes and uses A/B testing to assess decision quality, human-AI alignment, and changes in disagreement with AI recommendations.

## Project Links

- [Published RPubs report](https://rpubs.com/Angelina_yu/1440697)
- [R Markdown analysis source](analysis/AB-Test-Loan-Officer.Rmd)
- [Presentation PDF](presentation/AB-Test-New-AI-Model-Loan-Approval-Decisions.pdf)

## Business Question

Does the new AI model help loan officers reduce risky loan approvals and improve alignment with AI recommendations?

In this context, the primary business risk is approving bad loans that later default. The analysis therefore prioritizes reducing Final Type II Rate, while also checking whether loan officers become more aligned with AI recommendations after model assistance.

## Experiment Design

- Control group: loan officers using the legacy model
- Treatment group: loan officers using the new AI model
- Unit of analysis: loan officer
- Control sample: 10 loan officers, 100 observations
- Treatment sample: 28 loan officers, 280 observations

The raw decision records were aggregated to the loan-officer level to avoid treating repeated observations from the same officer as independent users.

## Metrics

| Metric | Purpose | Desired Direction |
| --- | --- | --- |
| Final Type II Rate | Share of bad loans incorrectly approved after model assistance | Lower is better |
| Type II Reduction | Improvement from initial to final Type II Rate | Higher is better |
| Agreement Lift | Increase in agreement between loan officers and AI recommendations | Higher is better |
| Conflict Reduction | Decrease in disagreement between loan officers and AI recommendations | Higher is better |

## Key Results

| OEC | Test | P-value | Significant | Effect Size | Interpretation |
| --- | --- | ---: | --- | --- | --- |
| Final Type II Rate | Welch's t-test | 0.0056 | Yes | d = 1.67, large | Treatment reduced Final Type II Rate |
| Type II Reduction | Wilcoxon | 0.2559 | No | r = 0.11, small | No evidence of greater Type II Reduction |
| Agreement Lift | Wilcoxon | 0.0049 | Yes | r = 0.411, moderate | Higher adoption of AI recommendations |
| Conflict Reduction | Wilcoxon | 0.0109 | Yes | r = 0.368, moderate | Lower disagreement with AI |

The treatment group reduced Final Type II Rate from 39.3% to 26.8%, a reduction of 12.5 percentage points compared with the control group. The primary metric was statistically significant with a large effect size, supporting deployment of the new model.

Type II Reduction was not statistically significant. The report notes that this may be explained by limited statistical power and baseline differences between the control and treatment groups.

## Repository Structure

```text
.
├── README.md
├── analysis/
│   └── AB-Test-Loan-Officer.Rmd
├── data/
│   └── data.csv
├── presentation/
│   └── AB-Test-New-AI-Model-Loan-Approval-Decisions.pdf
```

## Recommendations

- Adopt the new AI model based on the significant reduction in Final Type II Rate.
- Continue collecting data to improve statistical power.
- Use a more balanced future experiment design, ideally with 20-30 loan officers per group.
- Consider matched-pair or cross-over designs if sample size is limited.
