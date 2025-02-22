# Bank Term Deposit Subscription Prediction

## Overview
This project predicts whether a bank client will subscribe to a term deposit. Using a dataset of over 41,000 observations and 20+ features related to client demographics, campaign interactions, and economic indicators, the study applies both **Exploratory Data Analysis (EDA)** and **Extreme Gradient Boosting (XGBoost)** with various sampling strategies. A key part of the analysis involves a **cost-benefit framework** to assess the model’s real-world impact.

---

## Table of Contents
1. [Business Problem Understanding](#business-problem-understanding)  
2. [Data Description](#data-description)  
3. [Methodology](#methodology)  
4. [Modeling and Evaluation](#modeling-and-evaluation)  
5. [Cost-Benefit Analysis](#cost-benefit-analysis)  
6. [Conclusion](#conclusion)  
7. [Project Structure](#project-structure)  
8. [Getting Started](#getting-started)  
9. [Acknowledgments](#acknowledgments)

---

## Business Problem Understanding
- **Objective**: To build a classification model that predicts whether a bank customer will subscribe to a term deposit.
- **Business Value**: By accurately targeting potential subscribers, the bank can optimize its marketing spend and increase term deposit subscriptions.

---

## Data Description
- **Dataset**: Contains **41,188 records** and **20+ features** covering:
  - **Client Attributes** (age, job, marital status, etc.)
  - **Campaign/Marketing Attributes** (number of contacts, previous campaigns)
  - **Social/Economic Attributes** (consumer price index, consumer confidence index, euribor rate)
- **Target Variable**: `y`, indicating whether the client subscribed to a term deposit.

### Notable Data Characteristics
- Missing data for some categorical features is labeled as `unknown`.
- The dataset is **highly imbalanced**—most clients do **not** subscribe (over 36k) compared to those who do (approx. 4.6k).

---

## Methodology
1. **Exploratory Data Analysis (EDA)**  
   - Investigated distribution of subscribers vs. non-subscribers across generational cohorts, types of employment, loan status, etc.  
   - Visualized relationships between subscription rates and economic indices (e.g., consumer price index, consumer confidence index, euribor rate).
2. **Data Preparation**  
   - **Dummy Encoding**: Converted categorical features into dummy variables (one-hot encoding).  
   - **Handling Missing Values**: Kept as `unknown` to retain information rather than discarding.  
   - **Resampling Techniques**: Addressed class imbalance using:
     - Random Under-Sampling
     - Random Over-Sampling
     - SMOTE
     - SMOTE & Tomek Links
3. **Feature Selection & Transformation**  
   - Certain features were created or combined for clarity (e.g., combining or categorizing age groups into generational cohorts).
4. **Model Development: XGBoost with Bayesian Optimization**  
   - Employed **Extreme Gradient Boosting (XGBoost)** for its efficiency and strong performance in classification tasks.  
   - **Bayesian Optimization** was used to search for optimal hyperparameters, making the search process more efficient than traditional grid or random search.

---

## Modeling and Evaluation
- **Training**:  
  - Each resampled dataset (Under-Sampled, Over-Sampled, SMOTE, SMOTE & Tomek) was used to train a separate XGBoost model.
- **Validation**:  
  - Hyperparameters (learning rate, max depth, etc.) were tuned via Bayesian Optimization, using a validation set for iterative feedback.
- **Performance Metrics**:  
  - **Accuracy**: Proportion of correct predictions.  
  - **Precision & Recall**: Balance between how many predicted positives are correct (precision) and how many actual positives are identified (recall).  
  - **F1 Score**: Harmonic mean of precision and recall.  
  - **ROC AUC**: Measures how well the model distinguishes between classes across thresholds.

### Key Observations
- SMOTE & Tomek sampling often yielded strong performance, striking a good balance between precision and recall.
- Married couples, admin employees, and certain generations (Gen Y) are more likely to subscribe, implying key target segments for marketing.

---

## Cost-Benefit Analysis
A hypothetical cost-benefit framework was introduced to approximate real-world marketing expenses and gains:
- **Marketing/Administration Cost per Contact**: \$5  
- **Benefit from a Successful Term Deposit**: \$100  
- **Cost-Benefit Matrix**:  
  - **True Positive (TP)**: Subscriber predicted correctly → cost-benefit = \$0 (model does not re-contact them unnecessarily).  
  - **True Negative (TN)**: Non-subscriber predicted correctly → cost-benefit = \$95 (benefit \$100 minus \$5 contact cost).  
  - **False Positive (FP)**: Predicted subscriber but actually non-subscriber → cost-benefit = \-\$95.  
  - **False Negative (FN)**: Predicted non-subscriber but actually subscriber → cost-benefit = \-\$5.  

By applying the confusion matrix from each model to the cost-benefit matrix, the **expected profit** of the model can be computed and compared.

---

## Conclusion
- **Target Audience**: Married, Gen Y, and Admin job roles showed higher likelihood for subscription.  
- **Model Choice**: The **SMOTE & Tomek** XGBoost model was identified as the strongest candidate for deployment based on performance metrics and cost-benefit outcomes.  
- **Actionable Insight**: Marketing efforts can be more selectively focused, potentially saving on campaign costs while increasing subscription uptake.

---

## Project Structure
Below is a recommended layout for project files:
```
.
├── BLcase-study.pptx        # Presentation slides for high-level overview
├── BLCaseStudy.ipynb        # Jupyter Notebook with data analysis & modeling
├── README.md                # Project documentation (this file)
├── data/                    # Folder containing original CSV files
├── models/                  # Folder for trained model artifacts
└── reports/                 # Additional analysis outputs (figures, charts, etc.)
```

---

## Getting Started
1. **Clone the Repository**  
   ```bash
   git clone <your-repo-url>
   cd <your-repo-folder>
   ```
2. **Install Dependencies**  
   ```bash
   pip install -r requirements.txt
   ```
3. **Run the Analysis**  
   - Launch the Jupyter Notebook server:
     ```bash
     jupyter notebook
     ```
   - Open `BLCaseStudy.ipynb` and run the cells to reproduce the EDA, modeling, and results.
4. **View the Presentation**  
   - Open `BLcase-study.pptx` to see a concise, visual summary of the project approach and findings.

---

## Acknowledgments
- **Data Source**: Public dataset on bank marketing campaigns.  
- **Libraries**: [XGBoost](https://github.com/dmlc/xgboost), [Imbalanced-Learn](https://imbalanced-learn.org), [Bayesian Optimization (Hyperopt/BayesOpt, etc.)](https://github.com/hyperopt/hyperopt).

---

**Thank you for reviewing this project!** If you have any questions or suggestions, feel free to open an issue or reach out directly.
