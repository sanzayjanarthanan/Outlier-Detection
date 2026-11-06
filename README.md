# Task 28 – Outlier Detection (Employee Salary Dataset)

**Veda Technology · AI & ML Track · Level 1 · Day 28**

## Objective
Create a box plot for a numerical variable and identify possible outliers in the dataset, to understand basic outlier detection through visualization.

## Tools Used
- Python
- Pandas
- Matplotlib
- Jupyter Notebook

## Dataset
A small **sample (synthetic) Employee Salary dataset** created in code for this exercise. It is not real company data. It has 20 employees and 2 columns: `emp_id` and `salary` (in ₹), where salaries range from ₹32,000 to ₹2,20,000.

## Files in this Repository
| File | Description |
|------|-------------|
| `outlier_detection.ipynb` | Notebook with the box plot and outlier detection code |
| `employee_salary.csv` | Dataset used |
| `boxplot.png` | Box plot of salary |
| `README.md` | Approach, findings and explanation |

## 1. Box Plot

```python
plt.boxplot(data, vert=True)
plt.title("Box Plot of Employee Salary")
plt.ylabel("Salary (₹)")
```

![Box plot](boxplot.png)

In a box plot, the box spans Q1 to Q3 (the middle 50% of values), the line inside the box is the median, and the whiskers extend to the furthest values within 1.5 × IQR. Points beyond the whiskers are plotted individually as potential outliers.

## 2. Identifying Outliers (IQR Rule)

```python
Q1 = data.quantile(0.25)
Q3 = data.quantile(0.75)
IQR = Q3 - Q1
lower = Q1 - 1.5 * IQR
upper = Q3 + 1.5 * IQR
outliers = df[(data < lower) | (data > upper)]
```

| Measure | Value |
|---------|-------|
| Q1 | ₹40,750 |
| Q3 | ₹55,750 |
| IQR | ₹15,000 |
| Lower bound | ₹18,250 |
| Upper bound | ₹78,250 |

**Potential outliers identified:**

| emp_id | Salary |
|--------|--------|
| 19 | ₹1,85,000 |
| 20 | ₹2,20,000 |

Both values are far above the upper bound of ₹78,250. No value falls below the lower bound.

## 3. Effect of the Outliers

| Statistic | With outliers | Without outliers |
|-----------|---------------|------------------|
| Mean | ₹62,100 | ₹46,500 |
| Median | ₹47,000 | ₹45,500 |

## 4. Explanation of the Findings
1. **Two high-salary outliers.** The box plot shows two points far above the upper whisker. The IQR rule confirms them: ₹1,85,000 and ₹2,20,000 are well above the upper bound of ₹78,250.
2. **The mean is pulled by outliers, the median is not.** Removing the two values changes the mean by about ₹15,600 but the median by only ₹1,500. For data with outliers, the median describes a typical salary better than the mean.
3. **Outliers were not removed automatically.** An outlier is only *potentially* wrong. These two salaries could be data-entry errors, or they could be genuine senior or executive salaries. Genuine values carry real information and should be kept. The decision needs context about where the data came from.

## Key Learnings
- A box plot shows outliers quickly, and the IQR rule gives a numeric way to confirm them.
- Outliers affect the mean much more than the median.
- Detecting an outlier is not the same as deciding to delete it.

## Interview Questions – Key Answers
1. **What is an outlier?** A data point that lies far away from the rest of the values in a dataset.
2. **How can a box plot help identify outliers?** It shows the box (Q1 to Q3) and whiskers (up to 1.5 × IQR). Points outside the whiskers are plotted separately and are potential outliers.
3. **Should every outlier be removed?** No. Remove or fix it if it is an error. Keep it if it is a genuine but rare value, because removing it loses information. The decision depends on context.

## How to Run
```bash
pip install pandas matplotlib jupyter
jupyter notebook outlier_detection.ipynb
```
