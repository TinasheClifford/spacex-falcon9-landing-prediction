# SpaceX Falcon 9 First-Stage Landing Prediction

## Project Overview

This project investigates whether historical Falcon 9 launch characteristics can be used to predict the successful landing of SpaceX's first-stage booster.

The project was developed as part of the **IBM Data Science Professional Certificate capstone**, demonstrating an end-to-end data science workflow:

**Data Collection → Data Wrangling → Exploratory Data Analysis → SQL Analysis → Geospatial Analysis → Interactive Dashboard → Machine Learning**

### Central Business Question

> **Can historical mission characteristics be used to predict whether a Falcon 9 first stage will land successfully?**

Successful first-stage recovery is strategically important because rocket reusability can reduce launch costs. Understanding the characteristics associated with landing success can therefore support launch-risk analysis and cost estimation.

---

# Business Problem

SpaceX's Falcon 9 became commercially competitive partly through the reuse of its first-stage boosters.

For an organization evaluating the economics of competing with or bidding against SpaceX, an important question is whether the first stage of a launch is likely to be recovered successfully.

This project investigates:

* Which launch characteristics are associated with landing success?
* Does landing success vary by launch site?
* How does payload mass relate to landing outcomes?
* How does landing success change over time?
* Do different orbital missions have different landing outcomes?
* Can machine-learning classification models predict landing success?

---

# Project Objectives

## 1. Data Collection

Collect Falcon 9 launch information using:

* SpaceX API
* Web scraping

## 2. Data Wrangling

Clean, transform and prepare the launch data for exploratory analysis and machine learning.

## 3. Exploratory Data Analysis

Investigate relationships between landing success and:

* Launch site
* Payload mass
* Orbit
* Flight number
* Booster characteristics
* Mission date

## 4. SQL Analysis

Use SQLite and SQL queries to investigate launch records and operational mission characteristics.

## 5. Geospatial Analysis

Use Folium to investigate launch-site locations and their geographic context.

## 6. Interactive Analytics

Develop a Plotly Dash dashboard for interactive exploration of launch outcomes.

## 7. Predictive Analytics

Train and tune multiple classification algorithms to predict first-stage landing success.

---

# Data Collection

Two complementary data-collection approaches were used.

## SpaceX API

The SpaceX API was used to retrieve launch, payload, launch-site and booster information.

The workflow collected information including:

* Launch date
* Launch site
* Payload mass
* Orbit
* Booster information
* Landing outcome
* Booster reuse information
* Geographic coordinates

The API workflow successfully returned an HTTP **200** response.

## Web Scraping

Historical Falcon 9 launch information was also collected through web scraping.

The web-scraping workflow extracted launch records from HTML tables containing historical Falcon 9 mission information.

The two collection approaches provided complementary information that could subsequently be cleaned and transformed into an analytical dataset.

---

# Data Wrangling

The raw launch information contained multiple landing outcomes, including:

* Successful ocean landings
* Failed ocean landings
* Successful RTLS landings
* Failed RTLS landings
* Successful drone-ship landings
* Failed drone-ship landings
* No landing

A binary classification variable called **Class** was created:

| Class | Meaning                               |
| ----- | ------------------------------------- |
| `1`   | First stage landed successfully       |
| `0`   | First stage did not land successfully |

The final analytical dataset contained **90 Falcon 9 launch records**.

The resulting overall landing-success rate was:

### **82.22%**

This value was calculated from the binary landing classification variable.

---

# Exploratory Data Analysis

The EDA stage investigated how landing outcomes varied across mission characteristics using Python, Pandas, Matplotlib and Seaborn.

The analysis examined:

* Flight number
* Payload mass
* Launch site
* Orbit
* Landing success
* Mission year

## Flight Number and Payload Mass

The analysis compared flight number and payload mass while using landing outcome as the classification variable.

A clear pattern was observed:

> **Landing success generally increased as Falcon 9 accumulated more flight experience.**

The visualization also showed that successful landings occurred across a range of payload masses, indicating that payload mass alone does not explain landing success.

This suggests that **operational experience and mission characteristics should be considered together rather than treating payload mass as a standalone predictor.**

---

## Launch Site and Landing Outcome

The dataset contained launches from three primary launch sites:

| Launch Site  | Number of Launches |
| ------------ | -----------------: |
| CCAFS SLC-40 |                 55 |
| KSC LC-39A   |                 22 |
| VAFB SLC-4E  |                 13 |

CCAFS SLC-40 accounted for the largest share of observations.

Launch-site comparisons were therefore important for understanding how landing outcomes varied across operational locations.

---

## Payload Mass and Launch Site

The EDA also compared payload mass across launch sites.

One notable observation was:

> **Within this dataset, VAFB SLC-4E had no launches with payload mass greater than 10,000 kg.**

This is an observation about the historical dataset and should not be interpreted as a physical payload limitation of the launch site.

---

## Landing Success by Orbit

Landing success was compared across different orbital mission types.

The dataset contained missions targeting:

* GTO
* ISS
* VLEO
* PO
* LEO
* SSO
* MEO
* ES-L1
* HEO
* SO
* GEO

The resulting visualization showed that **landing success varied across orbit categories**.

This indicates that mission profile is an important analytical dimension when investigating first-stage recovery.

---

## Flight Number and Orbit

The project further investigated whether the relationship between flight experience and landing success was consistent across different orbital missions.

An important observation emerged:

> **LEO missions showed an apparent improvement in landing success as flight number increased, while GTO missions did not show an equally clear relationship.**

This suggests that the effect of operational experience may differ depending on the mission profile.

### Innovative Insight

**Experience does not necessarily affect every mission type in the same way.**

This interaction between **flight history and orbit** provides a more nuanced perspective than simply concluding that landing performance improved over time.

---

## Payload Mass and Orbit

Payload mass was also examined in combination with orbit and landing outcome.

The visualization showed successful landings across a range of payload masses.

In particular, relatively strong landing outcomes were observed for payloads associated with:

* Polar Orbit
* LEO
* ISS

GTO missions showed a more mixed pattern.

This reinforces an important analytical conclusion:

> **Payload mass alone is insufficient to explain landing success; mission orbit and other operational characteristics also matter.**

---

## Landing Success Over Time

The project calculated landing success by launch year.

The resulting trend showed:

> **Landing success increased from 2013 through 2020.**

This provides evidence of a strong temporal improvement in observed first-stage recovery performance.

The trend is consistent with increasing operational experience and technological development, although the analysis establishes an observed relationship rather than proving causation.

---

# Key EDA Findings

The exploratory analysis produced several important findings:

### 1. Landing performance improved over time

Later Falcon 9 flights generally exhibited higher landing success than earlier flights.

### 2. Mission profile matters

Landing success varied across orbital categories.

### 3. Launch site is an important analytical dimension

Landing outcomes differed across launch locations, making launch site a useful predictive feature.

### 4. Payload mass is not the whole story

Successful landings occurred across a wide range of payload masses.

### 5. Experience and mission type interact

The relationship between flight number and landing success appeared stronger for some orbital missions than others.

### 6. Landing success is a multi-factor problem

The EDA suggests that landing success should be evaluated using multiple variables rather than a single characteristic.

---

# SQL Analysis

The project used SQLite to perform structured analysis of the launch dataset.

## Selected SQL Findings

### Total Payload Carried for NASA CRS Missions

> **45,596 kg**

### Average Payload for F9 v1.1

> **2,928.4 kg**

### First Successful Ground-Pad Landing

> **22 December 2015**

### Successful Drone-Ship Landings with 4,000–6,000 kg Payloads

Four booster versions met the specified criteria:

* F9 FT B1022
* F9 FT B1026
* F9 FT B1021.2
* F9 FT B1031.2

The SQL analysis demonstrates how structured queries can be used to answer operational questions from a launch database.

---

# Geospatial Analysis with Folium

Folium was used to investigate the geographic distribution of Falcon 9 launch sites.

The interactive analysis included:

* Launch-site markers
* Success/failure markers
* Marker clustering
* Launch-site coordinates
* Proximity analysis
* Distance calculations

The launch locations represented in the analysis included:

* CCAFS LC-40
* CCAFS SLC-40
* KSC LC-39A
* VAFB SLC-4E

The analysis also investigated the geographic context surrounding launch sites, including proximity to:

* Coastlines
* Railways
* Highways
* Cities

This provided an additional geographic perspective on launch-site operations.

---

# Interactive Plotly Dash Dashboard

A Plotly Dash application was developed to transform the static analysis into an interactive analytical tool.

## Dashboard Features

### Launch-Site Filter

Users can select:

* All Sites
* CCAFS LC-40
* CCAFS SLC-40
* KSC LC-39A
* VAFB SLC-4E

### Landing Success Pie Chart

The dashboard dynamically displays successful and unsuccessful launch outcomes based on the selected launch site.

### Payload Range Slider

Users can interactively filter launches according to payload mass.

### Payload vs Landing Outcome

A scatter visualization allows users to investigate payload mass against landing outcome while distinguishing booster-version categories.

> **Note:** The original dashboard wording referred to this visualization as a "correlation" plot. For a portfolio version, it is more statistically appropriate to describe it as **Payload Mass vs Landing Outcome**, because the visualization alone does not establish statistical correlation or causation.

---

# Machine Learning

The landing-success problem was treated as a **binary classification problem**.

## Machine Learning Workflow

```text
Prepared Dataset
       ↓
Feature Selection
       ↓
Categorical Encoding
       ↓
Train/Test Split
       ↓
Feature Scaling
       ↓
Model Training
       ↓
GridSearchCV
       ↓
Model Evaluation
       ↓
Landing-Success Prediction
```

Four classification algorithms were evaluated:

1. Logistic Regression
2. Support Vector Machine
3. Decision Tree
4. K-Nearest Neighbors

Hyperparameters were optimized using:

**GridSearchCV with 10-fold cross-validation**

---

# Model Performance

| Model                  | Cross-Validation Score | Test Accuracy |
| ---------------------- | ---------------------: | ------------: |
| Logistic Regression    |                 84.64% |    **83.33%** |
| Support Vector Machine |                 84.82% |    **83.33%** |
| Decision Tree          |             **88.93%** |        77.78% |
| K-Nearest Neighbors    |                 84.82% |    **83.33%** |

## Selected Model

### Logistic Regression

Logistic Regression was selected as the final model based on held-out test performance.

Logistic Regression, SVM and KNN all achieved:

### **83.33% test accuracy**

The Decision Tree achieved the highest cross-validation score at **88.93%**, but its held-out test accuracy dropped to **77.78%**.

This demonstrates an important machine-learning principle:

> **A model with the highest cross-validation score is not necessarily the model that generalizes best to unseen data.**

For this project, model selection therefore considered **held-out test performance**, rather than relying solely on the highest validation score.

---

# Confusion Matrix Analysis

The Logistic Regression confusion matrix included:

* **12 true positives**
* **3 false positives**

The model correctly identified a substantial proportion of successful landing outcomes while also producing some false-positive predictions.

For a production-level system, accuracy alone would not be sufficient.

Additional evaluation should include:

* Precision
* Recall
* F1-score
* ROC-AUC
* Probability calibration

These metrics would provide a more comprehensive evaluation of the model's ability to distinguish successful and unsuccessful landings.

---

# Key Insights

## 1. Historical landing outcomes are highly informative

The analytical dataset recorded an overall landing success rate of **82.22%**.

This indicates that successful recovery was common within the historical missions represented in the dataset.

## 2. Landing performance improved over time

EDA showed an increasing landing-success trend as Falcon 9 accumulated more flights.

This suggests that operational experience and technological maturity are important considerations when interpreting historical recovery performance.

## 3. Mission profile matters

Landing success varied across orbital categories.

This indicates that the mission objective and orbital requirements may influence first-stage recovery outcomes.

## 4. Landing success is a multi-factor problem

The EDA suggests that no single variable should be used to explain landing success.

Potentially relevant factors include:

* Payload mass
* Orbit
* Launch site
* Flight history
* Booster configuration
* Reuse characteristics

## 5. Payload mass alone does not determine success

Successful landings occurred with both relatively light and heavy payloads.

Therefore, payload mass should be considered alongside other mission and booster characteristics.

## 6. Experience does not affect every mission equally

The EDA suggested a clearer relationship between flight number and landing success for LEO missions than for GTO missions.

This represents one of the project's more interesting exploratory insights and suggests that **mission type may interact with operational experience**.

## 7. Cross-validation performance does not guarantee test performance

The Decision Tree achieved the highest cross-validation score (**88.93%**) but performed worse on the held-out test dataset (**77.78%**).

This highlights the importance of evaluating generalization performance.

---

# Limitations

Several limitations should be considered when interpreting the results.

## Dataset Size

The analytical dataset contains only **90 Falcon 9 launch records**.

This limits the statistical power and generalizability of the predictive models.

## Historical Data

The dataset represents a historical period and therefore may not fully reflect current Falcon 9 operations.

## Missing Operational Variables

The dataset does not contain many potentially important variables, including:

* Detailed weather conditions
* Wind speed
* Atmospheric conditions
* Flight trajectory
* Detailed telemetry
* Autonomous flight-control information

These variables could potentially improve predictive performance.

## Classification Metrics

Accuracy alone does not provide a complete picture of model performance.

Future evaluation should include additional classification metrics, particularly because the dataset contains more successful than unsuccessful landing observations.

## Causality

Observed relationships between variables and landing success should not automatically be interpreted as causal relationships.

For example, the observed improvement in landing success over time does not by itself prove that flight number caused the improvement.

---

# Future Work

The project can be extended in several directions.

## 1. Weather Integration

Integrate historical weather information such as:

* Wind speed
* Temperature
* Precipitation
* Visibility
* Atmospheric pressure

This could provide additional information about environmental conditions during launch and landing.

## 2. Advanced Machine Learning

Evaluate additional algorithms such as:

* Random Forest
* Gradient Boosting
* XGBoost
* LightGBM

These models could potentially capture nonlinear relationships between mission characteristics and landing outcomes.

## 3. Probability-Based Predictions

Instead of returning only:

> Successful / Unsuccessful

the system could return a probability estimate such as:

> **Predicted landing success probability: 87%**

Probability-based predictions would be more useful for risk assessment and decision support.

## 4. Model Explainability

Use techniques such as:

* Feature importance
* SHAP
* Partial dependence

to investigate which variables contribute most strongly to model predictions.

## 5. Production Deployment

The trained model could eventually be deployed through an API and connected directly to the Dash application.

This would create an end-to-end system:

```text
Mission Information
        ↓
Data Processing
        ↓
Machine Learning Model
        ↓
Landing Probability
        ↓
Interactive Dashboard
```

---

# Technologies Used

## Programming

* Python
* SQL

## Data Collection

* SpaceX API
* Requests
* BeautifulSoup

## Data Analysis

* Pandas
* NumPy
* Matplotlib
* Seaborn

## Machine Learning

* Scikit-learn
* Logistic Regression
* Support Vector Machine
* Decision Tree
* K-Nearest Neighbors
* GridSearchCV

## Visualization

* Matplotlib
* Seaborn
* Plotly
* Folium
* Plotly Dash

## Database

* SQLite

---

# Project Structure

```text
spacex-falcon9-landing-prediction/
│
├── README.md
├── requirements.txt
│
├── notebooks/
│   ├── data-collection-api.ipynb
│   ├── webscraping.ipynb
│   ├── data-wrangling.ipynb
│   ├── eda-visualization.ipynb
│   ├── eda-sql.ipynb
│   ├── launch-site-location.ipynb
│   └── machine-learning-prediction.ipynb
│
├── dashboard/
│   └── spacex-dash-app.py
│
├── data/
│   ├── raw/
│   └── processed/
│
├── images/
│   ├── eda/
│   ├── folium/
│   ├── dashboard/
│   └── machine-learning/
│
└── docs/
    └── presentation.pdf
```

---

# Skills Demonstrated

This project demonstrates an end-to-end data science workflow involving:

* Data collection
* REST APIs
* Web scraping
* Data cleaning
* Data wrangling
* Exploratory data analysis
* SQL
* SQLite
* Geospatial analysis
* Interactive visualization
* Dashboard development
* Feature engineering
* Classification
* Hyperparameter tuning
* Cross-validation
* Model evaluation
* Data storytelling
* Business problem formulation

---

# Portfolio Takeaway

This project demonstrates how raw aerospace data can be transformed into analytical and predictive insights.

The workflow moves from:

> **Raw launch data**

to

> **Clean analytical dataset**

to

> **Exploratory insights**

to

> **Interactive analytics**

to

> **Machine-learning predictions**

The project also demonstrates several important data-science principles:

* Exploratory analysis can reveal relationships that are not obvious from raw data.
* Landing success is a multi-factor problem.
* Payload mass alone does not explain landing outcomes.
* Mission type and operational experience can interact.
* Cross-validation performance does not guarantee strong performance on unseen data.
* Interactive visualization can make analytical findings easier to explore and communicate.

Ultimately, the project demonstrates the ability to take a real-world business/engineering problem and develop an **end-to-end data science solution**, from data acquisition through predictive modeling and interactive visualization.

---

# Author

**Tinashe Clifford**

Mining Engineer | Data Science | Machine Learning | AI

Zimbabwe

[LinkedIn](#) · [GitHub](#)
