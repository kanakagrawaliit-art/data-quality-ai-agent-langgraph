# Agentic AI Data Quality Analysis & Recommendation Agent

An **Agentic AI system that automatically profiles CSV datasets, identifies potential data quality issues, and recommends corrective actions**.

Built with **Python, LangGraph, LangChain, OpenAI, Pydantic, and Pandas**, this project demonstrates how an AI agent can combine statistical data profiling with LLM reasoning to analyze the quality of a dataset and recommend how identified problems should be addressed.

## 🎯 What Does This Agent Do?

The agent accepts a **CSV file** as input and automatically examines its numerical and categorical features.

Instead of simply calculating statistics, the agent uses the results to identify potential **data quality problems** and generate recommendations for resolving them.

The workflow consists of four major stages:

**CSV Dataset → Data Profiling → Data Quality Analysis → Recommended Actions**

---

## 🔢 Numerical Column Analysis

For every numerical column, the agent analyzes statistics and distributions such as:

- Missing and null values
- Mean
- Median
- Mode
- Minimum and maximum values
- Quartiles
- Distribution of values
- Outliers
- Other unusual patterns in the data

These statistics allow the agent to understand the characteristics of each numerical feature and identify potential data quality concerns.

---

## 🔤 Categorical Column Analysis

For categorical features, the agent examines:

- Missing and null values
- Unique categories
- Category frequencies
- Distribution across categories
- Dominant or rare categories
- Potential inconsistencies in categorical values

This allows the system to understand how categorical data is distributed and identify potential quality problems.

---

## 🔍 Data Quality Issue Detection

After profiling the dataset, the agent combines findings from the numerical and categorical analyses.

It then evaluates the results to identify potential issues such as:

- Missing data
- Null values
- Numerical outliers
- Highly skewed distributions
- Unusual numerical ranges
- Rare categorical values
- Imbalanced categorical distributions
- Potentially inconsistent categories
- Other suspicious patterns in the dataset

The statistical analysis provides evidence to the agent, while the LLM reasoning layer interprets those findings in the context of data quality.

---

## 💡 Data Quality Recommendations

The agent does more than identify problems.

For every detected issue, it recommends an appropriate corrective action.

Depending on the problem, recommendations may include:

- Mean or median imputation
- Mode imputation
- Creating an `Unknown` category for missing categorical data
- Investigating or treating outliers
- Reviewing suspicious numerical values
- Standardizing inconsistent categories
- Combining rare categories when appropriate
- Removing problematic records or columns when justified
- Performing additional validation before using the dataset

The goal is to answer two questions:

> **What is wrong with this dataset?**

and

> **What should we do about it?**

---

## 🧠 Agentic Workflow

```text
                         START
                           │
                           ▼
                       Load CSV
                           │
              ┌────────────┴────────────┐
              │                         │
              ▼                         ▼
      Numerical Analysis       Categorical Analysis
              │                         │
      • Null / Missing          • Null / Missing
      • Mean                    • Unique Categories
      • Median                  • Frequencies
      • Mode                    • Distribution
      • Quartiles               • Rare Categories
      • Distribution            • Inconsistencies
      • Outliers                       │
              │                         │
              └────────────┬────────────┘
                           │
                           ▼
                    Combine Findings
                           │
                           ▼
                Identify Data Quality
                       Issues
                           │
                           ▼
                Recommend Corrective
                       Actions
                           │
                           ▼
                 Generate Data Quality
                       Report
                           │
                           ▼
                  Review & Score Report
                           │
                           ▼
                       Approved?
                      /         \
                    YES          NO
                     │            │
                     ▼            ▼
               Final Report    Feedback
                     │            │
                     ▼            │
                    STOP      Improve Report
                                  │
                                  └──► Review Again
