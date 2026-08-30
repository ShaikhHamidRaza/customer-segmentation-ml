# Customer Segmentation using K-Means Clustering

An unsupervised machine learning project that segments mall customers into distinct groups using **K-Means clustering**, based on age, annual income, and spending score.

The project focuses on turning customer-level data into interpretable customer segments that can support targeted marketing and customer strategy.

## Project Highlights

- Analyzed **1,000 customer records** from the Mall Customers dataset
- Handled missing values and verified duplicate records
- Removed **18 rows with missing values**, leaving **982 customers** for modeling
- Performed exploratory data analysis (EDA)
- Selected **Age, Annual Income, and Spending Score** as clustering features
- Applied **StandardScaler** before distance-based clustering
- Used the **Elbow Method** to select `k = 5`
- Evaluated cluster quality using **Silhouette Score**
- Built a K-Means model with `k = 5`
- Used **PCA** to visualize the cluster structure in two dimensions
- Analyzed cluster-level statistics to interpret customer segments

## Business Problem

Customers have different demographic characteristics, purchasing power, and spending behavior. Treating every customer as the same can make marketing strategies less targeted.

The objective of this project is to use unsupervised learning to identify groups of customers with similar characteristics and translate those groups into practical customer segments.

## Dataset

The project uses a **Mall Customers dataset** containing 1,000 customer records and five columns:

| Feature | Description |
|---|---|
| `CustomerID` | Unique customer identifier |
| `Gender` | Customer gender |
| `Age` | Customer age |
| `Annual Income (k$)` | Annual income in thousands of dollars |
| `Spending Score (1-100)` | Spending score assigned based on customer spending behavior |

### Data Preparation

The dataset initially contained:

- 1,000 rows
- 5 columns
- Missing values in `Gender`, `Age`, `Annual Income (k$)`, and `Spending Score (1-100)`
- No duplicate rows

Missing rows were removed, resulting in **982 complete records** used for clustering.

`Gender` was retained in the dataset but **was not used as a clustering feature**.

## Machine Learning Workflow

```text
Mall Customers Dataset
          ↓
Data Inspection
          ↓
Missing-Value & Duplicate Check
          ↓
Remove Missing Rows
          ↓
Exploratory Data Analysis
          ↓
Feature Selection
(Age, Income, Spending Score)
          ↓
StandardScaler
          ↓
Elbow Method
          ↓
Silhouette Score Evaluation
          ↓
K-Means (k = 5)
          ↓
Cluster Statistics
          ↓
PCA Visualization
          ↓
Customer Segment Interpretation
```

## Features Used for Clustering

The following three features were used:

- **Age**
- **Annual Income (k$)**
- **Spending Score (1-100)**

`CustomerID` was not used because it is an identifier rather than a behavioral feature.

`Gender` was not included in the final clustering feature set.

## Model Selection

### Elbow Method

The Elbow Method was used to examine the Within-Cluster Sum of Squares (WCSS) for `k = 1` through `10`.

The resulting curve suggested **5 clusters** as a reasonable choice based on the elbow point.

### Silhouette Score

Silhouette Score was also calculated for `k = 2` through `10`.

| Number of Clusters | Silhouette Score |
|---:|---:|
| 2 | 0.5726 |
| 3 | 0.4847 |
| 4 | 0.3809 |
| **5** | **0.3301** |
| 6 | 0.3192 |
| 7 | 0.3221 |
| 8 | 0.3248 |
| 9 | 0.3181 |
| 10 | 0.3073 |

The **highest Silhouette Score among the tested values was 0.5726 at `k = 2`**. However, the final model uses **`k = 5` based on the Elbow Method**, allowing a more granular customer segmentation.

This distinction is important: `k = 5` was selected as the project's segmentation choice, not because it produced the highest silhouette score.

## Final Model

```text
Algorithm: K-Means Clustering
Number of clusters: 5
Random state: 42
Initialization runs: 10
Preprocessing: StandardScaler
```

The final model assigns each of the 982 processed customers to one of five clusters.

## Cluster Profiles

The following profiles are based on the mean values produced by the final K-Means clustering:

| Cluster | Avg. Age | Avg. Income (k$) | Avg. Spending Score | Interpretation |
|---:|---:|---:|---:|---|
| 0 | 25.3 | 25.7 | 62.0 | Younger, lower-income, relatively high-spending |
| 1 | 67.8 | 108.4 | 4.4 | Older, high-income, very low-spending |
| 2 | 33.0 | 41.4 | 53.5 | Younger, lower-income, relatively high-spending |
| 3 | 38.9 | 61.4 | 42.0 | Middle-aged, medium-income, moderate-spending |
| 4 | 46.8 | 85.7 | 25.9 | Higher-income, lower-spending |

These descriptions are **interpretations of the cluster averages**, not predefined labels in the dataset.

## Key Business Insights

The segmentation reveals several distinct customer profiles:

- **Clusters 0 and 2:** Younger customers with lower average income but comparatively high spending scores.
- **Cluster 1:** Older customers with the highest average income but extremely low spending scores.
- **Cluster 3:** A relatively balanced group with medium income and moderate spending.
- **Cluster 4:** Higher-income customers whose spending score is considerably lower than their income level might suggest.

These profiles can help a business think about different approaches such as customer engagement, retention, personalized promotions, and premium-customer strategies.

> **Important:** The project identifies statistical segments; marketing actions should be validated with additional customer and business data before being used operationally.

## Exploratory Data Analysis

The notebook includes visual analysis of:

- Customer age distribution
- Annual income distribution
- Spending score distribution
- Income vs. spending score
- Correlation between numerical variables

## Cluster Visualization

The final clusters are visualized using:

1. **Annual Income vs. Spending Score** — shows the customer groups in the original feature space.
2. **PCA visualization** — reduces the standardized three-feature dataset to two principal components for easier visualization.

PCA is used here specifically for **visualization**, not as the input to the final K-Means model.

## Technologies Used

- Python
- Pandas
- NumPy
- Scikit-learn
- Matplotlib
- Seaborn
- Jupyter Notebook
- Git & GitHub

## Project Structure

```text
customer-segmentation/
│
├── customer_segmentation_fixed.ipynb
├── store_customers.csv
├── requirements.txt
├── .gitignore
└── README.md
```

### File Description

**`customer_segmentation_fixed.ipynb`**  
Contains data inspection, cleaning, EDA, feature selection, scaling, cluster selection, K-Means training, cluster analysis, and PCA visualizations.

**`store_customers.csv`**  
Input customer dataset required to reproduce the notebook.

**`requirements.txt`**  
Contains the Python packages required to run the project.

**`.gitignore`**  
Excludes unnecessary local files and environments from version control.

## How to Run

### 1. Clone the repository

```bash
git clone <your-repository-url>
cd <repository-folder>
```

### 2. Create a virtual environment

#### Windows

```bash
python -m venv venv
venv\Scripts\activate
```

#### macOS / Linux

```bash
python3 -m venv venv
source venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Start Jupyter Notebook

```bash
jupyter notebook
```

Open:

```text
customer_segmentation_fixed.ipynb
```

Make sure `store_customers.csv` is in the same directory as the notebook, then run the cells sequentially.

## Limitations

This project is a portfolio-level customer segmentation analysis and has several limitations:

- The clustering uses only three features.
- `Gender` is not included in the clustering model.
- The dataset does not contain actual transaction history, purchase frequency, or product-level information.
- K-Means assumes a cluster structure that is reasonably represented by centroid-based grouping.
- The Elbow Method and Silhouette Score do not guarantee that the resulting segments are optimal from a business perspective.
- The final `k = 5` choice prioritizes the segmentation structure suggested by the Elbow Method even though `k = 2` achieved the highest tested Silhouette Score.

## Future Improvements

Possible extensions include:

- Add purchase frequency and transaction-value features
- Include product-category and customer-lifetime-value information
- Compare K-Means with Hierarchical Clustering and DBSCAN
- Perform hyperparameter/cluster-sensitivity analysis
- Build an interactive segmentation dashboard with Streamlit
- Track cluster stability across different samples
- Integrate the segmentation output into a marketing workflow

## Conclusion

This project demonstrates an end-to-end **unsupervised learning workflow** for customer segmentation.

K-Means was used to create five customer groups after preprocessing and feature scaling. The Elbow Method supported the choice of `k = 5`, while Silhouette Score was used as an additional cluster-quality diagnostic. Cluster-level statistics and PCA visualizations were then used to interpret the resulting customer profiles.

The main takeaway is that clustering can transform basic customer attributes into interpretable segments, but meaningful business decisions require richer behavioral data and further validation.

## Author

**Shaikh Hamid Raza**

- GitHub: [ShaikhHamidRaza](https://github.com/ShaikhHamidRaza)
- LinkedIn: [shaikhhamidraza](https://linkedin.com/in/shaikhhamidraza)
