README.md
# 🚀 SpaceX Falcon 9 First Stage Landing Prediction  
### IBM Data Science Professional Certificate – Final Capstone Project  
**Author:** Nora Vieytes  

---

## 🧠 Project Overview  
This project aims to **predict whether the SpaceX Falcon 9 first stage will successfully land**.  
Accurate landing predictions allow commercial partners to estimate launch costs, which depend on booster reuse.

This repository contains **all notebooks, analysis steps, visualizations, SQL queries, machine learning models, and final presentation materials** used throughout the capstone project.

---

# 📂 Repository Structure

📁 SpaceX-Falcon9-Landing-Prediction
│
├── SpaceX_Falcon9_Landing_Prediction_Final.ipynb ← Final consolidated notebook
├── presentation.pdf ← Final project presentation
├── README.md ← Project documentation (this file)
└── other notebooks (optional)

yaml
Copy code

---

# 🗂️ 1. Data Collection  
Data was obtained from:

- SpaceX REST API  
- Web scraping of Falcon 9 launch records  
- CSV datasets provided by IBM Skills Network  

Data sources included launch metadata, payload mass, launch site, orbit, booster version, grid fins, landing pad, and final landing outcome.

---

# 🛠️ 2. Data Wrangling  
Main steps performed:

- Handling missing values  
- Standardizing categorical variables  
- Feature engineering  
- Extracting the target variable **Class** (1 = landing success, 0 = failure)  
- Creating dummy variables using **one-hot encoding**

Final dataset shape: **(90, 80)** after one-hot encoding.

---

# 🔍 3. Exploratory Data Analysis (EDA)

EDA was performed using Seaborn, Matplotlib, and Pandas to investigate relationships between:

- Payload mass and landing outcome  
- Launch site and success rate  
- Orbit types  
- Flight number trends  
- Booster version and reuse count  

Examples of visualizations created:

### Average success rate by launch site  
```python
sns.barplot(data=df, x="LaunchSite", y="Class")
Payload distribution by landing outcome
python
Copy code
sns.histplot(data=df, x="PayloadMass", hue="Class", kde=True)
🧾 4. SQL Exploratory Analysis
A SQLite database was created to run SQL queries such as:

Counting launch sites

Calculating average payload by orbit

Identifying first successful landing

Summarizing failures by year

Ranking boosters by performance

Example query:

sql
Copy code
SELECT LaunchSite, COUNT(*) as TotalLaunches, AVG(Class) as SuccessRate
FROM SPACEX
GROUP BY LaunchSite
ORDER BY SuccessRate DESC;
🗺️ 5. Interactive Visualizations
🌍 Folium Map
An interactive Folium map shows:

Every launch site

Landing success/failure markers

Geographic relationships (coastline, roads, distance indicators)

📊 Plotly Dash Dashboard
Dashboard components include:

Launch site dropdown

Payload range slider

Pie chart of success by site

Scatterplot: Payload vs. Success

This dashboard allows interactive exploration of key variables affecting landing outcome.

🤖 6. Machine Learning Models
The following models were trained and tuned using GridSearchCV:

Models evaluated
Logistic Regression

Support Vector Machine (SVM)

Decision Tree

K-Nearest Neighbors (KNN)

Best Model
Decision Tree Classifier

Achieved the highest test accuracy: ≈ 83.33%

Performed well with nonlinear relationships

SVM Results
Best kernel found: sigmoid

All models were evaluated using:

Test accuracy

Confusion matrix

Classification report

📈 7. Model Comparison
The performance of the four models was summarized using bar charts and tables comparing their test accuracy scores.

python
Copy code
results = pd.DataFrame({
    'Model': ['Logistic Regression', 'SVM', 'Decision Tree', 'KNN'],
    'TestAccuracy': [logreg_acc, svm_acc, tree_acc, knn_acc]
})
🧾 8. Final Presentation
The file presentation.pdf includes:

Executive Summary

Introduction

Methodology (Data Wrangling, EDA, SQL, ML)

Visual analysis

Folium maps

Dash dashboard

ML results

Conclusions

Designed for peer scientists reviewing the technical details of the project.

🧠 9. Key Insights
Payload mass affects landing likelihood, but not in a linear way

Certain launch sites have significantly higher success rates

Booster reuse count and grid fins are strong indicators of success

Machine learning models can reliably predict landing outcome

🏁 10. Conclusion
This project demonstrates the complete end-to-end data science workflow:

Data collection

Wrangling and cleaning

EDA and SQL analysis

Interactive mapping and dashboards

Machine learning classification

Model tuning and evaluation

The findings can support cost estimation for Falcon 9 launches and improve operational decision-making.
