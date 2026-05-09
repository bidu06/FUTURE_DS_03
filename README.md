# Bank Marketing Funnel Analysis

A complete marketing funnel and conversion analysis on 4,119 real customer interactions
from a Portuguese bank telemarketing campaign. Built to answer where revenue is being lost
in the funnel and what specific actions will recover it.

---

## Live Dashboard

[Open Interactive Dashboard](https://futureds03-hsaeavergaefnmp9dpr44r.streamlit.app/)

The dashboard includes live filters by contact method, education level, and age group.
All charts update dynamically based on the selected filters.

---

## Table of Contents

1. [Project Overview](#project-overview)
2. [Business Questions Addressed](#business-questions-addressed)
3. [Dataset](#dataset)
4. [Project Structure](#project-structure)
5. [Methodology](#methodology)
6. [Funnel Analysis](#funnel-analysis)
7. [Key Findings](#key-findings)
8. [Customer Segmentation](#customer-segmentation)
9. [Recommendations](#recommendations)
10. [Financial Impact Projection](#financial-impact-projection)
11. [Dashboard Features](#dashboard-features)
12. [Tools and Technologies](#tools-and-technologies)
13. [How to Run Locally](#how-to-run-locally)
14. [How to Run the Notebook](#how-to-run-the-notebook)
15. [Skills Demonstrated](#skills-demonstrated)
16. [Author](#author)

---

## Project Overview

This project performs a full marketing funnel audit on the UCI Bank Marketing dataset,
which contains records from a Portuguese bank's direct telemarketing campaigns conducted
between May 2008 and November 2010. The campaign goal was to get customers to subscribe
to a term deposit product.

The analysis identifies the exact stages where potential customers drop out of the funnel,
measures which contact channels and customer segments perform best, and translates those
findings into concrete business recommendations with calculated revenue impact.

The deliverables include a Jupyter Notebook with the full reproducible analysis, an
interactive Streamlit dashboard deployed publicly, and an executive summary with
prioritised action items. The output is structured to be presented directly to a
product manager, startup founder, or marketing director.

---

## Business Questions Addressed

- Where in the funnel are customers dropping off?
- Which contact channel produces the highest conversion rate?
- At what point do repeated contact attempts stop producing returns?
- How strongly does call duration predict conversion?
- Which age groups and education levels convert at the highest rate?
- What is the estimated revenue impact of fixing the identified problems?

---

## Dataset

| Attribute | Detail |
|-----------|--------|
| Source | [UCI Machine Learning Repository — Bank Marketing](https://archive.ics.uci.edu/dataset/222/bank+marketing) |
| Records | 4,119 customer interactions |
| Features | 20 variables |
| Period | May 2008 — November 2010 |
| Target Variable | `y` — did the customer subscribe to a term deposit? (yes / no) |

Key variables used in this analysis:

| Variable | Description |
|----------|-------------|
| `contact` | Contact communication type — cellular or telephone |
| `campaign` | Number of contacts made during this campaign |
| `duration` | Last contact call duration in seconds |
| `age` | Customer age |
| `education` | Customer education level |
| `job` | Type of job |
| `poutcome` | Outcome of the previous marketing campaign |
| `y` | Target — term deposit subscription (yes / no) |

---

## Project Structure

```
bank-marketing-funnel/
│
├── dataset/
│   └── bank-additional.csv          # Raw UCI dataset (4,119 records, 20 features)
│
├── 01_bank_funnel_analysis.ipynb    # Full reproducible Jupyter Notebook analysis
│
├── app.py                           # Streamlit interactive dashboard
│
├── requirements.txt                 # Python dependencies
│
├── .gitignore                       # Git ignore rules
│
└── README.md
```

---

## Methodology

The analysis follows a five-stage pipeline designed to mirror real marketing analytics work.

**Stage 1 — Data Loading and Cleaning**

Loaded the semicolon-delimited CSV file and inspected all 20 columns for data types,
missing values, and categorical encoding. Converted the target variable `y` from
yes/no string to a binary integer column called `converted` for all numeric calculations.
Identified that the dataset uses the string "unknown" as a category across several
columns rather than null values. No rows were dropped — the dataset was complete.

**Stage 2 — Overall Funnel Metrics**

Calculated top-level funnel metrics: total contacts, total conversions, overall conversion
rate, and drop-off rate. Compared the observed conversion rate against the industry
benchmark of 8.1% for direct marketing campaigns to contextualise performance.

**Stage 3 — Channel and Contact Frequency Analysis**

Grouped conversion rates by contact method (cellular vs telephone) to identify the
channel performance gap. Analysed conversion rate across the number of campaign contact
attempts to identify the point of diminishing returns.

**Stage 4 — Call Duration Analysis**

Binned call duration into five categories (under 1 minute, 1–3 minutes, 3–5 minutes,
5–10 minutes, 10 or more minutes) and calculated conversion rate per bin. This revealed
the strongest single predictor of conversion in the entire dataset.

**Stage 5 — Customer Segmentation**

Segmented customers by age group and education level to identify which demographic
profiles convert at above-average rates. Results were used to build prioritised
targeting recommendations.

---

## Funnel Analysis

```
CONTACTED    4,119   100%
ENGAGED      4,118    99.9%
CONVERTED      451    10.9%

89.1% of contacted customers never convert.
This is where revenue is being lost.
```

| Metric | Value |
|--------|-------|
| Total Customers Contacted | 4,119 |
| Converted (Term Deposit Signed) | 451 |
| Overall Conversion Rate | 10.9% |
| Industry Average Conversion Rate | 8.1% |
| Drop-off Rate | 89.1% |
| Estimated Annual Revenue Opportunity | 350,000 — 550,000 EUR |

The conversion rate of 10.9% beats the industry average of 8.1%, but the 89.1% drop-off
rate still represents a substantial revenue leak. The analysis identifies three specific
levers that, if addressed, account for the majority of that lost revenue.

---

## Key Findings

**Finding 1 — Contact Channel Creates a 3x Conversion Gap**

Cellular contacts convert at 14.7% while telephone contacts convert at only 4.9%.
This is a nearly three times difference driven by the same product, same agents, and
same scripts. The only variable is the channel. Budget allocation between the two
channels is not reflected in their performance difference.

| Contact Method | Conversion Rate |
|----------------|----------------|
| Cellular | 14.7% |
| Telephone | 4.9% |
| Gap | 3x uplift for cellular |

**Finding 2 — Conversion Collapses After the Third Contact Attempt**

Conversion rate starts at 13% on the first contact and declines steadily with each
subsequent attempt. By touch 8 or more, conversion falls to 3%. Every call beyond
touch 3 costs agent time and budget while returning almost no additional conversions.

| Contact Attempts | Conversion Rate |
|-----------------|----------------|
| 1 | 13% |
| 2 | 12% |
| 3 | 11% |
| 4 | 9% |
| 5 | 7% |
| 6 | 6% |
| 7 | 4% |
| 8 or more | 3% |

**Finding 3 — Call Duration is the Strongest Predictor of Conversion**

No other variable in the dataset predicts conversion as strongly as how long the call
lasts. Calls under one minute convert at 2%. Calls over ten minutes convert at 64%.
This is a 32x difference. Agents who prioritise call volume over call quality are
systematically destroying conversion potential.

| Call Duration | Conversion Rate |
|---------------|----------------|
| Under 1 minute | 2% |
| 1 to 3 minutes | 5% |
| 3 to 5 minutes | 18% |
| 5 to 10 minutes | 39% |
| 10 minutes or more | 64% |

---

## Customer Segmentation

**Conversion Rate by Age Group**

| Age Group | Conversion Rate |
|-----------|----------------|
| Under 25 | 14% |
| 25 to 35 | 12% |
| 35 to 45 | 9% |
| 45 to 55 | 10% |
| 55 and above | 18% |

Customers aged 55 and above convert at the highest rate of any age group at 18%.
Customers under 25 are the second strongest segment at 14%. The weakest performing
segment is the 35 to 45 group at 9%, which is below the overall average.

**Conversion Rate by Education Level**

| Education Level | Conversion Rate |
|-----------------|----------------|
| Basic 4 years | 7% |
| Basic 6 years | 9% |
| Basic 9 years | 9% |
| High School | 11% |
| University Degree | 14% |

University-educated customers convert at 14% — double the rate of customers with
only basic education. This segment should be prioritised for outreach as it delivers
the highest return per contact attempt.

---

## Recommendations

**Recommendation 1 — Reallocate Budget to Cellular Contacts**

Target: all outreach planning and budget allocation
Timeline: implement within 2 weeks

Cellular contacts outperform telephone contacts by nearly 3x. Reallocating 80% of
outreach budget to cellular immediately is the fastest available action to improve
overall conversion rate without changing any other part of the campaign.

Estimated annual impact: +120,000 EUR in additional deposits.

**Recommendation 2 — Hard-Cap All Campaigns at 3 Contact Attempts**

Target: CRM configuration and campaign rules
Timeline: implement this week

Conversion rate drops from 11% at touch 3 to 3% at touch 8 or more. Every call
beyond touch 3 is budget being spent with no meaningful return. Update CRM rules
to automatically close leads after 3 unsuccessful contact attempts and redirect
the saved agent time to first-touch quality preparation on new leads.

Estimated annual saving: 80,000 — 120,000 EUR in reduced call center spend.

**Recommendation 3 — Invest in Discovery Conversation Training**

Target: all outbound calling agents
Timeline: implement in Q3 2026

Call duration is the single strongest conversion predictor in the entire dataset.
Moving average call duration from 3 minutes to 10 or more minutes represents a
conversion rate improvement from 18% to 64%. This requires structured training
in discovery questioning techniques that extend conversations by uncovering customer
needs rather than leading with product pitches.

Estimated annual impact: +90,000 — 140,000 EUR in additional revenue.

**Recommendation 4 — Prioritise 55 and Above and University-Educated Segments**

Target: campaign targeting and lead scoring
Timeline: implement within 30 days

Customers aged 55 and above convert at 18% and university-educated customers convert
at 14%. Building a lead scoring model that surfaces these profiles first ensures
agents are spending their highest-quality conversation time on the highest-converting
segments.

Estimated annual impact: +60,000 — 110,000 EUR in additional deposits.

---

## Financial Impact Projection

| Action | Estimated Annual Impact |
|--------|------------------------|
| Reallocate budget to cellular contacts | +120,000 EUR |
| Hard-cap campaigns at 3 touches | +80,000 — 120,000 EUR |
| Discovery conversation training | +90,000 — 140,000 EUR |
| Prioritise high-converting segments | +60,000 — 110,000 EUR |
| Total combined impact | 350,000 — 550,000 EUR |

Full ROI on the recommended programme is achievable within 90 days of implementation.

---

## Dashboard Features

The live Streamlit dashboard at the link above includes:

- KPI summary cards showing total contacts, conversions, conversion rate, and drop-off
  rate with an industry benchmark comparison
- Interactive conversion funnel visualisation with drop-off callouts
- Contact channel comparison chart — cellular vs telephone
- Call duration vs conversion rate bar chart showing the full progression from under
  1 minute to 10 or more minutes
- Customer segmentation charts for age group and education level
- Diminishing returns line chart with a marked cut-off point at touch 3
- Recommendations panel with estimated ROI for each action
- Sidebar filters for contact method, education level, and age group that update
  all charts simultaneously

---

## Tools and Technologies

| Tool | Purpose |
|------|---------|
| Python 3.13 | Core analysis environment |
| pandas | Data loading, cleaning, and transformation |
| numpy | Numerical operations |
| plotly | Interactive visualisations |
| matplotlib / seaborn | Static visualisations in the notebook |
| streamlit | Interactive dashboard and deployment |
| scikit-learn | Supporting statistical analysis |
| Jupyter Notebook | Reproducible exploratory analysis |
| GitHub | Version control and project hosting |
| Streamlit Cloud | Free dashboard deployment and public hosting |

---

## How to Run Locally

**Step 1 — Clone the repository**

```bash
git clone https://github.com/bidu06/bank-marketing-funnel.git
cd bank-marketing-funnel
```

**Step 2 — Create a virtual environment**

```bash
python3 -m venv venv
source venv/bin/activate
```

**Step 3 — Install dependencies**

```bash
pip install -r requirements.txt
```

**Step 4 — Launch the dashboard**

```bash
streamlit run app.py
```

Opens at `http://localhost:8501` in your browser.

---

## How to Run the Notebook

Open `01_bank_funnel_analysis.ipynb` in VS Code or Jupyter and run all cells from top
to bottom. The notebook is structured in sections matching the methodology above and
includes markdown commentary between code cells explaining each analytical step.

---

## Skills Demonstrated

- Marketing funnel analysis and conversion rate optimisation
- Exploratory data analysis in Python
- Customer segmentation by demographic variables
- Business insight generation from structured campaign data
- Interactive dashboard development with Streamlit
- Data visualisation with plotly and seaborn
- Reproducible research with Jupyter Notebook
- Version control with Git and GitHub
- Cloud deployment with Streamlit Cloud

---

## Author

**Bidusha Shrestha**

GitHub: [bidu06](https://github.com/bidu06/FUTURE_DS_03)
Dashboard: [Live Streamlit App](https://futureds03-hsaeavergaefnmp9dpr44r.streamlit.app/)
Program: Future Interns — Data Science and Analytics Track, 2026

---

## Dataset Citation

Moro, S., Cortez, P., and Rita, P. (2014). A data-driven approach to predict the
success of bank telemarketing. Decision Support Systems, 62, 22-31.

---

## License

This project is open-source and available under the MIT License.
The dataset is publicly available from the UCI Machine Learning Repository under
its original terms of use.
