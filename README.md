# SaaS churn analysis – junior data analyst project

This repository contains a case study I worked on as a junior data analyst.  
The goal is to understand customer churn in a B2B SaaS company and build a first simple churn prediction model.

I structured the project in two main notebooks:

- `saas_project_cleaning_merging.ipynb` – data understanding, cleaning, feature engineering, and merging.
- `saas_project_exploration.ipynb` – exploratory analysis and modeling on the cleaned dataset.

---

## Objective

Churn is a key topic for SaaS businesses because losing customers directly reduces recurring revenue.

In this project, I wanted to:

- learn how to work with several operational datasets at the same time,
- create a clean analytical dataset at account level,
- explore which customer segments seem more at risk of churn,
- and test a few basic models to predict churn.

This is not a production‑ready model, but a learning exercise to show a complete junior data analyst workflow.

---

## Data used

The project uses several tables that represent typical SaaS data:

- **Accounts** – industry, company size, country, acquisition channel, account creation date.
- **Subscriptions** – plan type (Free, Pro, Enterprise), MRR in USD, subscription start and end dates.
- **Usage** – product feature usage (feature name, events count, active users, event date).
- **Support tickets** – ticket category (Billing, Bug, Feature request, Onboarding), status, satisfaction score.
- **Churn labels** – churn outcome at account level (`churned` True / False).

I do not design the data; I work with it as if it came from a SaaS company data warehouse.

---

## Notebook 1 – Cleaning and merging

`saas_project_cleaning_merging.ipynb`

In this notebook, I focus on:

- Inspecting each table to understand shapes, types and basic issues.
- Converting date fields to datetime (for example, `account_created_at` and subscription dates).
- Handling missing values with simple, transparent rules (for example, dropping rows with missing churn labels).
- Creating a few features at account level, such as:
  - `issmallcompany` (1–10 and 11–50 employees vs the rest),
  - `dayssincecreated`, `monthssincecreated`, `yearssincecreated` (tenure),
  - `EU` vs `Non EU` region.
- Checking basic distributions (country counts, plan types, number of tickets, satisfaction scores).
- Merging the cleaned tables into a single dataset where each row represents one account.

The idea here is to show that I can:

- go from raw tables to a tidy analytical dataset,
- document my cleaning decisions,
- and prepare features that make sense from a business point of view.

---

## Notebook 2 – Exploration and modeling

`saas_project_exploration.ipynb`

In this notebook, I use the merged dataset to:

### Exploratory data analysis

- Look at the class balance between churned and non‑churned accounts.
- Explore churn rates by:
  - industry,
  - company size,
  - acquisition channel (Inbound, Outbound, Partner, Self‑serve),
  - small vs non‑small companies,
  - EU vs Non‑EU region.
- Identify which segments seem to have higher churn and could be interesting for the business.

I try to keep the visualizations simple and focus on interpretations that a non‑technical stakeholder could understand.

### Modeling

Then I build and compare three models:

- Logistic Regression,
- Random Forest,
- XGBoost.

Because churn is a binary problem and the classes are not perfectly balanced, I pay more attention to:

- F1‑score,
- precision,
- recall,

than to accuracy alone.

In this case study:

- XGBoost gives the best F1‑score,
- Logistic Regression is a good baseline,
- Random Forest performs less well with the current features.

I do not claim that this is the best possible model; my aim is to show that I understand how to:

- split data,  
- train models,  
- choose metrics,  
- and compare results.

---

## What this project shows about my skills

As a junior data analyst, this project is meant to demonstrate that I can:

- Work with several tables and join them into a coherent dataset.
- Clean data and create simple, useful features (tenure, size, region, etc.).
- Use Python and common libraries (pandas, NumPy, scikit‑learn, xgboost, matplotlib / seaborn).
- Perform basic exploratory analysis and explain what I see in the data.
- Build and evaluate simple classification models with appropriate metrics for an imbalanced problem.
- Write markdown and comments that tell a clear story instead of just showing code.

---

## How to run the project

1. Clone the repository:

```bash
git clone <your-repo-url>
cd <your-repo-folder>
```

2. (Optional) Create and activate a virtual environment:

```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. Install the main dependencies:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn xgboost
```

4. Start Jupyter Notebook or JupyterLab:

```bash
jupyter notebook
```

5. Open and run the notebooks in this order:

- `saas_project_cleaning_merging.ipynb`
- `saas_project_exploration.ipynb`

---

## Possible next steps

If I continue this project, I would like to:

- Add more detailed usage features (for example, frequency and intensity per feature).
- Try other techniques for handling class imbalance (resampling, class weights).
- Build a simple app or dashboard (for example with Streamlit) to show churn risk by segment.
- Improve documentation and make the analysis more interactive for non‑technical users.
