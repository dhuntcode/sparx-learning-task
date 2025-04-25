# Sparx Data Analysis Task

## Description

This project contains a Jupyter Notebook (`sparx_analysis_notebook.ipynb` or similar) that performs an analysis of student assessment and homework activity data provided for a technical task. The analysis addresses mandatory questions about student progress and comparisons, an exploratory question about the potential impact of Sparx usage on performance, and a stretch question about using activity data for personalization.

## Setup Instructions

### Prerequisites

* **Python:** Version 3.12 or higher recommended.
* **Poetry:** A Python dependency management and packaging tool. ([Installation Guide](https://python-poetry.org/docs/#installation))
* **Git:** (Optional, but recommended for version control).

### Installation

1.  **Install Dependencies:**
    Navigate to the project's root directory in your terminal (the one containing the `pyproject.toml` file and the `data` subdirectory with the data files). Run Poetry to create a virtual environment and install the required libraries:
    ```bash
    poetry install
    ```
    This command reads the `pyproject.toml` file, resolves dependencies (including pandas, numpy, matplotlib, seaborn, scipy, pyarrow, jupyterlab, and potentially statsmodels if added), and installs them into an isolated environment. Ensure the `data` folder containing `task_qla_df.csv` and `task_tia_df.feather` is present in the same directory where you run this command, as the notebook expects it at `../data/`.

## Running the Notebook

1.  **Activate Environment & Launch JupyterLab:**
    From the project's root directory in your terminal, use Poetry to launch JupyterLab. This automatically activates the correct virtual environment.
    ```bash
    poetry run jupyter lab
    ```
    This command should open JupyterLab in your default web browser.

    **Troubleshooting (Snap Confinement Issue):** If you encounter a "Permission Denied" or "Access Denied" error relating to a file in a `.local/share/jupyter/runtime` directory (especially if using VS Code installed via Snap), JupyterLab might be blocked from automatically opening the browser tab. Use this command instead:
    ```bash
    poetry run jupyter lab --no-browser
    ```
    Then, copy the URL provided in the terminal output (it will look like `http://localhost:8888/lab?token=...`) and paste it into your web browser manually.

2.  **Open and Run Notebook:**
    * In the JupyterLab interface, navigate to and open the analysis notebook file (e.g., `sparx_analysis_notebook.ipynb`).
    * You can run the cells sequentially by selecting a cell and pressing `Shift + Enter` or by using the "Run" menu options.

## Summary of Findings

*(Based on the current state of the notebook execution)*

* **Q1: Common Students:** 1394 distinct students have both assessment and activity data.
* **Q2: Mean Progress:** For students with at least two assessments, the mean progress (change in percentage score) between consecutive assessments was approximately -2.59%. *(Note: Exact value depends on the final execution)*.
* **Q3: Progress Distribution:** A histogram/density plot visualizing the distribution of progress values was generated.
* **Q4: First vs. Second Test Performance:**
    * 1388 students were compared after handling missing data.
    * Mean score on the first assessment: ~53.51%; Mean score on second assessment: ~50.92%.
    * Mean difference (Second - First): ~-2.59%.
    * A paired t-test indicated this difference is statistically significant (p < 0.05), suggesting students performed significantly worse on their second assessment compared to their first in this dataset.
* **Q5: Improving Confidence:** Confidence in the Q4 result could be improved by controlling for confounding variables like assessment difficulty or time between tests using statistical models.
* **Exploratory Question (Sparx Usage & Performance):**
    * An analysis framework was set up to explore the link between Sparx usage (total correct answers) and performance on the second assessment, controlling for the first assessment score.
    * **Note:** The regression model execution (using `statsmodels`) is currently commented out in the notebook. Running this model is required to determine the specific association found.
    * **Conclusion:** Any conclusion about whether Sparx usage is associated with improved performance requires running the regression model. Even with a result, this observational analysis cannot prove causation due to potential confounding factors (motivation, teaching, etc.).
* **Stretch Question (Personalization):**
    * Activity data can be modelled (e.g., using Logistic Regression) to predict student struggle on specific topics/tasks based on features like historical success, time spent, etc.
    * These predictions can enable personalized interventions (adjusting task difficulty, offering support) even without assessment data, leveraging the rich activity logs.

