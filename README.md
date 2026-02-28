# Robot Navigation Analysis Package

---

## Table of Contents

- [Installation](#installation)
- [Required Changes](#required-changes)
- [Usage](#usage)
- [Output Files](#output-files)

---

# Installation

## 1. Clone or Download

Navigate to the `assignment4` directory. It should look like this:

## Project Structure

```
assignment4/
├── images/                         # Output folder for generated graphs
├── output/                         # Output folder for generated files
├── setup/
│   ├── __init__.py
│   ├── config.py                   # Update your configs here
│   ├── test_setup.py               # Script to test the env
│   └── requirements.txt            # All Dependencies needed to run this project
├── src/
│   ├── logBasedPackage/            # LOG-BASED files
│   │   ├── __init__.py
│   │   ├── anomaly.py
│   │   ├── context.py
│   │   ├── features.py
│   │   ├── geometry.py
│   │   ├── log_analysis.py
│   │   ├── pattern_mining.py
│   │   ├── preprocessing.py
│   │   └── relation_analysis.py
│   ├── scenarioBasedModelPackage/  # SCENARIO-BASED files
│   │   ├── customScenarios/        # New generated Custom Scenarios
│   │   ├── scenarioHelper/
│   │   │   ├── __init__.py
│   │   │   └── helper.py
│   │   ├── __init__.py
│   │   ├── aggregator.py
│   │   ├── runScenarioBasedModel.py
│   │   ├── scenario_level_eval.py
│   │   └── scenarioBasedModel.py
│   ├── __init__.py
│   └── data_loading.py             # Common for 2 modes
├── main.py                         # Main script and eentry point of the whole SW
├── README.md
├── task.md
└── team_1_project_submission.md
```

# 2. Create Virtual Environment (Optional but Recommended)

1. Install Python 3.10 from ```python.org/downloads```, or check your python version: ```python --version ; python3.10 --version```
2. Navigate to project folder
3. Create virtual environment: /usr/local/bin/python3.10 -m venv .final_assign ;``` /opt/homebrew/bin/python3.10 -m venv .final_assign```
4. Activate virtual environment: ```source .final_assign/bin/activate```
5. verify python version: ```python --version```
6. Upgrade pip: ```pip install --upgrade pip```


From now on your dependencies will be installed within this environment and not globally.
# 3. Install Dependencies

Navigate to setup directoy, then install all dependencies via : ```pip install -r requirements.txt```
Required Changes

## 1. Data Paths (CRITICAL)

As the dataset is not part of our repo, you MUST update its path in config.py before running:
```# In config.py - UPDATE THESE PATHS!
DATA_ROOT = ASSIGN4_ROOT / "../ws25_aia_te_dataset/ws25_aia_complete_data"
MAPS_DETAILS_PATH = ASSIGN4_ROOT / "../ws25_aia_te_dataset/maps_details.json"
```
## 2. Memory Settings (Optional)

If you have limited RAM (< 16GB), you should update ```max_samples``` when using class in ```MemoryEfficientPatternMiner in main.py```. You can do it by adjusting the ```max_samples``` to be less than 50K (for example 30K):
```
# In main.py
pattern_miner = MemoryEfficientPatternMiner(
    temporal_weight=0.6,
    max_samples=30000,  # Reduced from 50000 if low memory
    use_sampling=True,
    dtype='float32'
)
```
# Usage
#### Pre-checks
Before running the SW, run the script ```assignment4/setup/test_setup.py``` to perform some pre-checks on the environment:

```
python test_setup.py
```

We have 2 modes in this assignment: Scenario-based or Log-based. You can run them together or seperate as follows:

## Scenario-based prediction mode
```
python main.py --scenario-based
```
or for the newly generated custom scenarios:
```
python main.py --custom-scenario-based
```
## Log-based prediction mode
```
python main.py --log-based
```
## Both modes

This is for running the whole assignment (both scenario-based and log-based) no arguments should be given. Note: custom-scenario-based doesn't run in this mode, you have to run it seperatly
```
python main.py
```

## Output Files

The pipeline generates structured data outputs and reports in assignment4/output, and visualizations in assignment4/images.

# assignment4/output

## CSV Files

```> LOG_BASED_analyzer_runs_df.csv ``` – Per-run summaries extracted from log-based analysis

```> LOG_BASED_analyzer_runs_anomalies.csv``` – Per-run anomaly summaries detected from logs

```> LOG_BASED_analyzer_summary_df.csv``` – Aggregated statistics across all log-based runs

```> LOG_BASED_final_df_with_contexts.csv``` – (Not uploaded due to its srotage) Dataset augmented with extracted spatial and contextual information

```> LOG_BASED_final_df_with_features.csv``` – (Not uploaded due to its srotage) Dataset enriched with engineered features

```> LOG_BASED_final_df_with_anomalies.csv``` – (Not uploaded due to its srotage) Dataset annotated with detected anomalies

```> LOG_BASED_anomaly_feature_vectors.csv``` – (Not uploaded due to its srotage) Full feature vectors extracted at anomaly points

```> LOG_BASED_anomaly_feature_vectors_clustered_lite.csv``` – (Not uploaded due to its srotage) Reduced / clustered anomaly feature vectors

```> LOG_BASED_feature_relation_df.csv``` – (Not uploaded due to its srotage) Feature–relation mapping used for relation analysis

```> LOG_BASED_context_specific_patterns.csv``` – Patterns discovered within specific spatial or semantic contexts

```> LOG_BASED_context_specific_relation_performance.csv``` – Relation performance metrics per context

```> LOG_BASED_context_temporal_stats.csv``` – Temporal statistics of context occurrences

```> LOG_BASED_global_patterns.csv``` – Globally discovered behavioral or relational patterns

```> LOG_BASED_relation_frequency_analysis.csv``` – Frequency analysis of relations across runs

```> LOG_BASED_relation_anomaly_correlation.csv``` – Correlation between relations and detected anomalies

```> LOG_BASED_relation_predictive_power.csv``` – Predictive power metrics of relations

```> SCENARIO_VS_LOG_level_comparison.csv``` – Quantitative comparison between scenario-based and log-based predictions

# Reports (TXT)

```> LOG_BASED_relation_generalization_report.txt``` – Textual report summarizing relation generalization, predictive behavior, and failure modes

```> SCENARIO_BASED_anomaly_predictions.txt``` – Scenario-based anomaly predictions

```> SCENARIO_BASED_env_features.txt``` – Extracted environment-level features used in scenario modeling

```> CUSTOM_SCENARIO_BASED_anomaly_predictions.txt``` – Custom-Scenario-based anomaly predictions

```> CUSTOM_SCENARIO_BASED_env_features.txt``` – Extracted environment-level features used in custom scenarios modeling

```> output.log``` – Terminal log

# assignment4/images

## Visualizations (PNG)

### Log-Based Global Analysis

```> LOG_BASED_cluster_visualization_lite.png``` – PCA-based visualization of clustered anomaly feature vectors

```> LOG_BASED_relation_generalization_overview.png``` – High-level overview of relation generalization

```> LOG_BASED_relation_generalization_predictive_detail.png``` – Detailed predictive performance per relation

```> LOG_BASED_Correlation - Behavior Ground Truth vs Log Semantic Failure.png``` – Correlation between ground truth behaviors and log-derived semantic failures

```> LOG_BASED_Success-Failure Proportion per Scenario.png``` – Scenario-level success vs failure distribution

```> LOG_BASED_Total Mission Outcomes.png``` – Aggregate mission outcome statistics

### Context & Relation Visualizations

```> LOG_BASED_corridor_contexts_boxes.png``` – Spatial visualization of corridor-related contexts

```> LOG_BASED_single_context_ctx_global.png``` – Example visualization of a single global context

```> LOG_BASED_top_failure_contexts_boxes.png``` – Spatial distribution of the most failure-prone contexts

### Trajectory & Alignment Analysis

```> LOG_BASED_Trajectory Analysis_small-dataset-maps-0-3-door-width-1f1-1 - Run 0.png``` – Trajectory analysis for door-width scenario

``` > LOG_BASED_Alignment Check_small-dataset-maps-0-3-door-width-1f1-1 - Run 0.png``` – Map–trajectory alignment verification

### Scenario-Based Analysis

``` > SCENARIO_BASED_ALL_anomaly_distribution.png``` – Distribution of anomalies predicted by the scenario-based model

``` > CUSTOM_SCENARIO_BASED_anomaly_distribution.png``` – Distribution of anomalies predicted by the custom-scenario-based model

``` > SCENARIO_VS_LOG_cmp_confusion_matrix.png``` – Confusion matrix comparing scenario-based vs log-based predictions







