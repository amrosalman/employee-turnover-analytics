# Employee Turnover Analytics

An end-to-end machine-learning project that analyzes employee-turnover patterns, predicts employee attrition, segments employees by risk, and recommends targeted retention strategies.

## Project Overview

Portobello Tech wants to better understand why employees leave and identify employees who may be at risk of turnover.

This project uses employee satisfaction, evaluation scores, project workload, monthly working hours, company tenure, promotion history, department, salary, and other employee characteristics to:

* Perform data-quality checks
* Explore factors associated with turnover
* Cluster employees who left
* Handle class imbalance using SMOTE
* Train and compare three classification models
* Select the best-performing model
* Assign employees to turnover-risk zones
* Recommend targeted retention strategies

## Dataset

The original dataset contained:

* 14,999 employee records
* 10 variables
* 0 missing values
* 3,008 exact duplicate rows

After duplicate removal, the cleaned dataset contained:

* 11,991 unique employee records
* 10 variables

### Main Variables

* `satisfaction_level`
* `last_evaluation`
* `number_project`
* `average_montly_hours`
* `time_spend_company`
* `Work_accident`
* `left`
* `promotion_last_5years`
* `Department`
* `salary`

The `left` variable is the prediction target:

* `0` means the employee stayed
* `1` means the employee left

## Project Workflow

1. Loaded and inspected the employee dataset
2. Checked missing values and duplicate records
3. Validated categorical, binary, and numerical values
4. Performed exploratory data analysis
5. Created a numerical correlation heatmap
6. Analyzed employee satisfaction, evaluation, and working-hours distributions
7. Compared project workloads for employees who stayed and left
8. Applied K-means clustering to employees who left
9. Encoded categorical variables using one-hot encoding
10. Created an 80:20 stratified train-test split
11. Applied SMOTE to handle class imbalance
12. Trained three machine-learning models
13. Used leakage-safe five-fold cross-validation
14. Compared model performance using multiple metrics
15. Created ROC curves and confusion matrices
16. Selected the best model
17. Assigned employees to turnover-risk zones
18. Recommended retention strategies

## Exploratory Data Analysis Findings

Employee satisfaction had the strongest numerical relationship with turnover, with a correlation of approximately `-0.35`.

Employees with lower satisfaction levels were generally more likely to leave.

The project-count analysis showed a nonlinear relationship between workload and turnover:

* Employees with three or four projects were more likely to stay
* Employees with only two projects showed higher turnover
* Employees with six or seven projects also showed higher turnover

This suggests that both underutilization and excessive workloads may contribute to employee turnover.

## Employee Clustering

K-means clustering divided employees who left into three groups:

| Cluster | Employees | Satisfaction | Evaluation | Description                                              |
| ------- | --------: | -----------: | ---------: | -------------------------------------------------------- |
| 0       |       534 |        0.111 |      0.869 | Highly dissatisfied, high-performing employees           |
| 1       |       555 |        0.806 |      0.913 | Highly satisfied, high-performing employees              |
| 2       |       902 |        0.410 |      0.517 | Moderately dissatisfied employees with lower evaluations |

The clustering results show that turnover is not limited to one employee profile.

## Machine-Learning Models

The following classification models were trained:

* Logistic Regression
* Random Forest Classifier
* Gradient Boosting Classifier

SMOTE was placed inside the cross-validation pipeline to prevent data leakage.

## Model Performance

| Model               | Accuracy | Precision | Recall | F1 Score | ROC-AUC |
| ------------------- | -------: | --------: | -----: | -------: | ------: |
| Logistic Regression |   77.57% |    41.21% | 82.41% |   54.94% |  83.18% |
| Random Forest       |   97.12% |    91.86% | 90.70% |   91.28% |  97.35% |
| Gradient Boosting   |   95.96% |    85.08% | 91.71% |   88.27% |  97.71% |

## Best Model

Random Forest was selected as the best overall model.

It achieved:

* 97.12% accuracy
* 91.86% precision
* 90.70% recall
* 91.28% F1 score
* 97.35% ROC-AUC

Although Gradient Boosting achieved slightly higher recall and ROC-AUC, Random Forest provided the strongest balance between identifying employees who may leave and limiting false-positive alerts.

## Confusion Matrix Results

The Random Forest model produced:

* 1,969 true negatives
* 32 false positives
* 37 false negatives
* 361 true positives

This means the model correctly identified 361 of the 398 employees who left.

## Employee Risk Zones

The selected Random Forest model assigned employees to four risk zones:

| Risk Zone        | Employees | Percentage |
| ---------------- | --------: | ---------: |
| Safe Zone        |     1,836 |     76.53% |
| Low-Risk Zone    |       188 |      7.84% |
| Medium-Risk Zone |        45 |      1.88% |
| High-Risk Zone   |       330 |     13.76% |

A total of 375 employees were classified in the Medium- or High-Risk zones.

## Retention Strategies

### Safe Zone

* Maintain regular employee engagement
* Recognize employee contributions
* Continue development opportunities
* Gather periodic employee feedback

### Low-Risk Zone

* Monitor satisfaction and workload
* Conduct manager check-ins
* Clarify career-development opportunities
* Review changes in employee engagement

### Medium-Risk Zone

* Conduct targeted stay interviews
* Review workload and compensation
* Create employee-development plans
* Address role or management concerns

### High-Risk Zone

* Begin immediate retention intervention
* Conduct confidential stay interviews
* Review compensation and promotion opportunities
* Adjust workload where appropriate
* Create personalized retention plans

## Technologies Used

* Python
* Jupyter Notebook
* Visual Studio Code
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Scikit-learn
* Imbalanced-learn
* SMOTE
* K-means clustering

## Repository Contents

```text
employee-turnover-analytics
├── project_screenshots
├── Employee_Turnover_Analytics.ipynb
├── Employee_Turnover_Project_Writeup.docx
├── employee_turnover_risk_results.csv
├── HR_comma_sep.csv
├── .gitignore
└── README.md
```

## How to Run the Project

1. Clone the repository.

```bash
git clone https://github.com/amrosalman/employee-turnover-analytics.git
```

2. Open the project folder.

```bash
cd employee-turnover-analytics
```

3. Create a Python virtual environment.

```bash
python -m venv .venv
```

4. Activate the environment on Windows PowerShell.

```powershell
.\.venv\Scripts\Activate.ps1
```

5. Install the required packages.

```bash
python -m pip install pandas numpy matplotlib seaborn scikit-learn imbalanced-learn jupyter ipykernel
```

6. Open `Employee_Turnover_Analytics.ipynb` in VS Code or Jupyter Notebook.

7. Select the `.venv` Python kernel.

8. Restart the kernel and run all notebook cells.

## Limitations

* The dataset does not contain a unique employee identifier.
* Exact duplicate rows were treated as duplicate observations.
* The analysis identifies predictive relationships but does not prove causation.
* Additional factors such as manager quality, benefits, commute distance, employee engagement, and external job opportunities were not included.
* Model predictions should support HR decisions, not replace professional judgment.

## Conclusion

The project demonstrates how machine learning can help HR identify employees who may be at risk of leaving.

Random Forest provided the strongest overall performance and was used to assign employees to turnover-risk zones. The resulting insights can support earlier, more targeted, and evidence-based employee-retention decisions.
