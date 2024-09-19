
# Email Marketing Campaign Analysis

## Problem Formulation

In the area of **marketing**, email is a go-to method for promoting products. It is **cheap**, **fast**, and **effective**. Most marketers run an experiment to see whether or not their email-marketing strategy works.

In this domain, I would like to analyze whether **emailing affects revenue** by observing the spending of each customer. We'll look at **factors that can predict spending** (in the following weeks).

During a period of two weeks following the e-mail campaign, results were tracked.  job is to tell the world if the Mens or Womens e-mail campaign was successful.

## Data Description

This dataset contains 64,000 customers who last purchased within twelve months. The customers were involved in an e-mail test.
- 1/3 were randomly chosen to receive an e-mail campaign featuring Mens merchandise
- 1/3 were randomly chosen to receive an e-mail campaign featuring Womens merchandise
- 1/3 were randomly chosen to not receive an e-mail campaign

The following columns are most used for analysis:

- **Customer ID**: Unique identifier for each customer.
- **Email Opened**: Whether the customer opened the email or not.
- **Email Clicked**: Whether the customer clicked on the email content or not.
- **Total Spend**: Total spending of the customer.
- **Week**: Week of the observation period.

### Features:
- **Email Opened** and **Email Clicked**: Binary variables (0 = No, 1 = Yes) representing user interaction.
- **Total Spend**: Continuous variable indicating the amount spent by each customer.

## Objective

The objective of the analysis is to:

1. **Understand the impact of email marketing on customer spending.**
2. **Predict the spending pattern** of customers based on their email activity.
3. **Identify any trends** that could help improve future email marketing campaigns.

## Causal Analysis

### What is Causal ML?

**Causal Machine Learning (Causal ML)** focuses on understanding and estimating causal effects rather than just correlations. It aims to answer questions like "What is the impact of an email campaign on customer spending?" by modeling the cause-and-effect relationship between variables. Unlike traditional machine learning, which might find associations, Causal ML seeks to determine whether one variable directly influences another.

### Methods Used

- **Propensity Score Matching**: Estimates treatment effects by matching treated and untreated units that have similar characteristics. This helps control for confounding variables that might affect the outcome.
- **Difference-in-Differences (DiD)**: Compares changes in outcomes over time between a treatment group (e.g., customers who received an email) and a control group (e.g., customers who did not receive an email) to estimate the causal impact of the treatment.
- **Instrumental Variables (IV)**: Uses instruments (variables related to the treatment but not directly affecting the outcome) to account for unobserved confounding factors.
- **Causal Inference Models**: Advanced models such as those in the `DoWhy` library combine various methods and assumptions to provide robust causal estimates. These models can incorporate structural causal models and adjust for multiple confounders.

## Steps of Analysis

### 1. Data Exploration

We will begin by **exploring the data**:
- **Check for Missing Values**: Ensure the dataset is complete or handle missing data appropriately.
- **Distribution of Key Variables**: Understand the distribution of variables like `Email Opened`, `Email Clicked`, and `Total Spend`.
  - **Histograms**: Show the distribution of `Total Spend` to identify spending patterns.
  - **Bar Charts**: Display the frequency of `Email Opened` and `Email Clicked` to understand customer interaction rates.

### 2. Data Preprocessing

Before applying any models, we need to:
- **Handle Missing Values**: Impute or remove missing data.
- **Convert Categorical Features**: Convert `Email Opened` and `Email Clicked` into numerical values (e.g., 0 and 1).
- **Normalize/Standardize Data**: Normalize `Total Spend` to ensure consistency in model performance.

### 3. Exploratory Data Analysis (EDA)

We will perform EDA to:
- **Visualize Distributions**: Use various plots to understand the distribution of variables.
  - **Boxplots**: Compare `Total Spend` across different email interaction categories (e.g., `Email Opened` and `Email Clicked`).
  - **Scatterplots**: Examine the relationship between `Email Clicked` and `Total Spend`.
- **Analyze Relationships**: Identify how email interactions affect `Total Spend`.
  - **Pair Plots**: Show the relationships between `Email Opened`, `Email Clicked`, and `Total Spend` to identify patterns and correlations.

### 4. Feature Engineering

We will create new features based on existing data:
- **Interaction Features**: Combine `Email Opened` and `Email Clicked` to analyze the effects of different interaction patterns.
- **Week-based Features**: Include temporal features to capture variations in customer behavior over different weeks.

### 5. Model Building

We will build models to predict customer spending:
- **Linear Regression**: Predict `Total Spend` based on email interactions.
- **Logistic Regression** or **Decision Trees**: Classify whether email interactions lead to increased spending.
- **Causal ML Models**: Estimate the causal impact of email interactions on spending using methods such as Propensity Score Matching, DiD, and IV.

### 6. Evaluation

We will evaluate the models using metrics like:
- **R-squared**: For regression models, assess the proportion of variance explained.
- **Accuracy, Precision, and Recall**: For classification models, evaluate the prediction performance.
- **Causal Metrics**: Analyze causal effects using Average Treatment Effect (ATE) or Conditional Average Treatment Effect (CATE) to understand the impact of email campaigns on spending.

## Conclusion

Based on the analysis and modeling results, we aim to:
- Draw conclusions about the **effectiveness** of email marketing.
- Provide actionable insights for **optimizing future campaigns**.
- Summarize key findings and offer **recommendations** to enhance email marketing strategies.

## Tools Used

The analysis will be performed using the following tools:
- **Python** for data analysis and model building.
- **Pandas** and **NumPy** for data manipulation.
- **Matplotlib** and **Seaborn** for data visualization.
- **Scikit-learn** for machine learning model implementation.
- **DoWhy** and **EconML** for causal inference and analysis.

## Conclusion
We run randomized experiments and do not observe any significant heterogeneity effects across the observed groups. This is validated by simple balancedness checks, heterogeneity checks, and uplift-modelling giving estimates that are close to the Average Treatment Effect.

**Results from Hypothesis Test:** Our initial findings showed that the available email-campaign data is close to a Randomized Controlled Trial, where there are no biases observed amongst the treatment and control groups. We find that there was a significant increase in average spending of the group who were sent emails regarding products for men compared to customers who were not sent emails. The conditional treatment effect is non-existent here. This is observed by using various Regressors (CausalML & DoWhy), where the treatment effect (after accounting for confounders) is close to the Average Treatment Effect.
