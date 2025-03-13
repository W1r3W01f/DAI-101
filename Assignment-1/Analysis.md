# DAI-101 Assignment-01 Solution Analysis Report
**Dataset:** ks-projects-201801.csv  

## Introduction  
This report presents the process of data cleaning and exploratory data analysis (EDA) on the **Kickstarter Projects dataset**. The dataset contains information about various crowdfunding campaigns, including project goals, pledged amounts, categories, and states (successful, failed, etc.).  

**Objective:**  
- Clean the dataset by handling missing values, duplicates, outliers, and inconsistent formatting.  
- Perform EDA to uncover distributions within the data using univariate, bivariate and multivariate analysis.

---

## Data Cleaning  

### Dataset Overview  
- Number of rows: 378,661
- Number of columns: 15  
- Key columns: `name`, `category`, `main_category`, `currency`, `deadline`, `goal`, `pledged`, `state`, `backers`, etc.  

### Handling Missing Values  
- **Columns with missing values:**  
  - `name`: 4 missing values (dropped)  
  - `usd pledged`: 3797 missing values (replaced with median value)  

### Removing Duplicates  
- **Duplicates found:** 0   
- No duplicate rows were detected.  

### Detecting and Treating Outliers  
- Used **Interquartile Range (IQR)** method to identify outliers in the `goal` column.  
- **Outliers removed:** Used Z-score test to remove the outliers.

### Scaling data  
- Used **Min-Max Scaling** to normalise `usd_pledged_real`, `usd_goal_real`and `pledged` columns.

---

## Exploratory Data Analysis (EDA)  

### Univariate Analysis  

**Summary Statistics:**  

| Statistic  | ID           | Goal (USD)    | Pledged (USD) | Backers   | USD Pledged | USD Pledged Real | USD Goal Real |
|------------|---------------|---------------|---------------|-----------|-------------|------------------|---------------|
| Count      | 378,285       | 378,285       | 378,285       | 378,285   | 378,285     | 378,285          | 378,285       |
| Mean       | 1.0753e+09    | 26,557.47     | 0.000476      | 105.71    | 6,972.50    | 0.000446         | 0.006832      |
| Std. Dev.  | 6.1908e+08    | 164,965.50    | 0.004704      | 907.62    | 78,272.74   | 0.004475         | 0.029441      |
| Median     | 1.0753e+09    | 5,100.00      | 0.000031      | 12.00     | 394.77      | 0.000031         | 0.001563      |
| Mode       | 5,971         | 5,000.00      | 0.00          | 0.00      | 0.00        | 0.000000         | 0.001429      |
| Variance   | 3.8326e+17    | 2.7214e+10    | 2.2128e-05    | 823,775.7 | 6.1266e+09  | 2.0021e-05        | 8.6680e-04    |
| Skewness   | -0.0026       | 82.83         | 75.13         | 86.72     | 106.43      | 82.18            | 16.22         |

**Insights:**  
- The `goal` amounts are **highly right-skewed** with extreme outliers, indicated by a skewness of **82.83**.  
- The majority of `pledged` values are close to **zero** — the median is **0.000031** — showing many projects receive little to no funding.  
- There’s a large gap between the **mean and median** for both `goal` and `pledged`, confirming the presence of outliers.  
- The `backers` column shows most projects have few supporters, but some outliers have up to **219,382** backers.  

---

### Bivariate Analysis  

**Correlation:**  
- Goal vs Pledged: **0.063** (weak positive correlation)  
- Backers vs Pledged: **0.72** (strong positive correlation)  

**Insights:**  
- There is a strong positive correlation (0.72) between pledged amounts and backers implying more backers generally result in higher pledges.
- The goal amount has little to no correlation with pledged amounts (0.015) suggesting that setting a high goal doesn’t guarantee more support.
- The weak correlation between USD Pledged and USD Goal (0.078) shows that projects often fail to reach their goals, aligning with the right-skewed goal distribution.

**Visulaisation**
- To keep the analysis relevant as well as easy to comprehened we just take into account the top categorical columns for the bar, violin and box plots.

### Multivariate Analysis  

- We randomly take 7000 samples to consider for the various pair plots just to see the nature of distribution without extensive computation.

**Grouped Comparisons and Insights:**

**Pledged Amount by Main Category and State:**
- Categories like Design and Technology have some extreme outliers in the pledged amounts, suggesting that a few projects might be pulling the average up.
- Music and Art categories show lower pledged amounts, possibly indicating smaller funding requirements or less engagement compared to technology-driven categories.

**Goal Amount by Main Category and State:**
- Categories like Games, Technology, and Design tend to have higher goal amounts, likely reflecting the higher costs associated with these projects.
- Crafts and Food projects have generally lower goal amounts, suggesting more modest funding needs.

**Statistic Analysis**
- P-value: 1.82e-99 — The extremely small p-value shows that the differences between groups are statistically significant.

## Conclusion

- Most projects set modest goals (around $2,000), but there are extreme outliers aiming for hundreds of thousands of dollars.
- Failed projects outnumber successful ones, especially in Technology and Design.
- Weak correlation between goal amounts and pledged funds — having a high goal doesn’t guarantee high pledges.
- Music and Film & Video have the highest success rates.
- Campaigns with lower goals (under $5,000) show the highest success rates, highlighting the importance of realistic goal-setting.

