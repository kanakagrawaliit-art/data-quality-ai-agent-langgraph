# Data Quality AI Agent with LangGraph | Elute Insights

> **AI-powered data quality analysis and recommendation agent built with Python, LangGraph, LangChain, and OpenAI.**

Elute Insights is a consulting business helping organizations turn data analytics, machine learning, and AI agent solutions into practical business outcomes. This repository demonstrates a LangGraph-based AI agent that profiles CSV datasets, identifies potential data quality issues, generates actionable recommendations, and evaluates its own recommendations through structured feedback.

The solution is designed as a transparent, workflow-oriented prototype for teams exploring **AI agent development**, **data quality assessment**, **automated analytics**, and **machine learning-enabled decision support**.

## Why Data Quality Matters

Poor data quality can affect reporting accuracy, business decisions, model performance, downstream integrations, and customer trust. Data professionals often need more than a list of missing values—they need an understandable explanation of what is wrong, why it may matter, and what should be done next.

This project combines:

- Statistical profiling of numerical and categorical data
- AI-assisted interpretation of data quality findings
- Actionable recommendations for data cleaning and preprocessing
- Structured feedback and scoring of generated recommendations
- A reusable LangGraph workflow for future AI agent development

## What the Agent Does

The project accepts a CSV dataset and performs the following workflow:

1. **Loads the dataset** from the working directory as `data.csv`.
2. **Profiles numeric columns** for counts, missing values, uniqueness, mean, median, standard deviation, ranges, interquartile range, and skewness.
3. **Profiles categorical columns** for counts, missing values, unique values, dominant categories, and category distributions.
4. **Combines the profiling results** into a single analysis context.
5. **Uses an OpenAI model** to generate a data quality report and recommendations for each column.
6. **Reviews the report through structured feedback** using a Pydantic model that returns a score from 1 to 10 and written improvement feedback.
7. **Repeats the recommendation cycle** when the score is below the acceptance threshold, stopping after the configured iteration limit.

The result is a structured AI-assisted workflow that can help teams identify data issues and improve the quality and usefulness of recommendations over multiple iterations.

## Technology Stack

- **Python** for application logic and data processing
- **Pandas** and **NumPy** for CSV profiling and statistical analysis
- **LangGraph** for orchestrating the AI agent workflow and state transitions
- **LangChain** and **LangChain OpenAI** for invoking the language model
- **OpenAI** for structured recommendation generation and evaluation
- **Pydantic** for validated structured output
- **python-dotenv** for environment configuration
- **Jupyter Notebook** for an interactive demonstration

## Project Structure

```text
.
├── main.ipynb
├── data.csv
├── requirements.txt
└── README.md
```

- `main.ipynb` contains the complete interactive LangGraph implementation.
- `data.csv` provides the sample dataset used by the agent.
- `requirements.txt` lists the Python packages required to run the project.
- `README.md` documents setup, workflow, and usage.

## How the LangGraph Workflow Works

The notebook defines a `StateGraph` with the following nodes:

```text
START
  ↓
Load CSV
  ├── Numerical Analysis
  └── Categorical Analysis
          ↓
      Combine Findings
          ↓
 Generate Recommendations
          ↓
 Evaluate Recommendations
          ↓
   Score ≥ 8 or Iteration Limit
          ├── END
          └── Improve Recommendations
```

The graph uses shared state to pass the loaded dataframe, profiling results, recommendation report, feedback, score, and iteration history between nodes. This makes the workflow easy to extend with additional analysis steps, validation rules, human approval gates, or data governance checks.

## Features

### Data Profiling

The agent analyzes numerical and categorical columns to identify:

- Missing and null values
- Data completeness and uniqueness
- Mean, median, and standard deviation
- Minimum and maximum values
- Quantiles and interquartile range
- Skewness and distribution characteristics
- Dominant values and category frequency
- Rare or unusual categories

### AI Recommendation Generation

An LLM interprets the profiling results and produces a recommendation for every column. The recommendations are designed to explain:

- Potential data quality concerns
- Specific corrective actions
- The reasoning behind each recommendation
- Whether no action is required
- How previous feedback should influence future output

### Structured Evaluation

The feedback node uses a structured output model to collect:

- Written feedback on the recommendation report
- A human-style score from 1 to 10
- A quality signal that can determine whether another recommendation cycle is needed

### Iterative Improvement

The workflow can review and revise recommendations when the score is below the selected threshold. The current implementation stops when either:

- The score is at least 8, or
- The recommendation iteration count exceeds 3

This loop can be adapted for a client-specific quality threshold, maximum number of iterations, or approval process.

## Prerequisites

Before running the notebook, you need:

- Python 3.10 or later
- An OpenAI-compatible API key
- An internet connection for model calls
- A CSV file named `data.csv` in the project directory

> The current notebook expects the API key in the `.env` file under the variable name `OPENAI_KEY`.

## Installation

From the project directory, create and activate a virtual environment:

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

Create a `.env` file in the project directory:

```dotenv
OPENAI_KEY=your_openai_api_key
```

Alternatively, use the `OPENAI_API_KEY` variable consistently in your environment configuration before running the notebook.

## Run the Demo

1. Place the CSV dataset in the project directory as `data.csv`.
2. Add your OpenAI API key to `.env` using `OPENAI_KEY`.
3. Open `main.ipynb` in VS Code or Jupyter Notebook.
4. Select the project Python environment as the notebook kernel.
5. Run the cells in sequence.
6. Review the generated recommendation report and feedback score.

The graph can also be visualized as a Mermaid diagram from the notebook and invoked through the compiled LangGraph application.

## Expected Input and Output

### Input

The agent expects a CSV file containing the dataset to analyze. The current implementation reads the file from the working directory using:

```python
pd.read_csv("data.csv")
```

### Output

The final invocation returns a dictionary containing fields such as:

- `recommendation_report`
- `feedback_report`
- `score`
- `recommendation_history`
- `feedback_history`
- `score_history`
- `counter`

The notebook currently displays the final `feedback_report` value in the last cell.

## Example Use Cases

This solution can support:

- Customer or operational dataset quality assessment
- Sales and revenue data validation
- Data preparation before machine learning
- Automated reporting and data cleaning recommendations
- AI-assisted quality review for business intelligence datasets
- Prototype development for data analytics and AI agent services

## Elute Insights Services

Elute Insights provides consulting support for:

- Data analytics and business intelligence
- Machine learning and predictive modeling
- AI agent solutions and workflow automation
- Data quality evaluation and preprocessing
- AI-assisted reporting and decision support

The company is founded by **Kanak Agrawal**, and you can contact the team at **kanak@eluteinsights.com**.

## About Elute Insights

Elute Insights helps businesses turn complex data and AI capabilities into practical, measurable solutions. The company works with organizations that want to improve data reliability, automate repetitive analysis, and explore AI-driven workflows while maintaining clear business context and human oversight.

This repository is a technical demonstration of the approach. It is not a complete production platform by itself; organizations should add appropriate security controls, data governance, monitoring, access management, and client-specific validation before deployment.

## License

This project is shared as a technical demonstration for Elute Insights. Review the repository's licensing terms before using or deploying the solution in a commercial environment.

## Connect with Elute Insights

For consulting inquiries, project discussions, or AI agent engagements, contact:

- **Email:** kanak@eluteinsights.com
- **Business:** Elute Insights
- **Focus:** Data analytics, machine learning, and AI agent solutions
