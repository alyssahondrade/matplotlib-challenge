# matplotlib-challenge
Module 5 Challenge - UWA/edX Data Analytics Bootcamp

Github repository at: [https://github.com/alyssahondrade/matplotlib-challenge.git](https://github.com/alyssahondrade/matplotlib-challenge.git)

## Table of Contents
1. [Introduction](https://github.com/alyssahondrade/matplotlib-challenge/blob/main/README.md#introduction)
    1. [Goal](https://github.com/alyssahondrade/matplotlib-challenge/blob/main/README.md#goal)
    2. [Repository Structure](https://github.com/alyssahondrade/matplotlib-challenge/blob/main/README.md#repository-structure)
    3. [Dataset](https://github.com/alyssahondrade/matplotlib-challenge/blob/main/README.md#dataset)
2. [Approach](https://github.com/alyssahondrade/matplotlib-challenge/blob/main/README.md#approach)
    1. [Prepare the data](https://github.com/alyssahondrade/matplotlib-challenge/blob/main/README.md#prepare-the-data)
    2. [Generate summary statistics](https://github.com/alyssahondrade/matplotlib-challenge/blob/main/README.md#generate-summary-statistics)
    3. [Create bar and pie charts](https://github.com/alyssahondrade/matplotlib-challenge/blob/main/README.md#create-bar-and-pie-charts)
    4. [Calculate quartiles, find outliers, and create a box plot](https://github.com/alyssahondrade/matplotlib-challenge/blob/main/README.md#calculate-quartiles-find-outliers-and-create-a-box-plot)
    5. [Create a line and scatter plot](https://github.com/alyssahondrade/matplotlib-challenge/blob/main/README.md#create-a-line-and-scatter-plot)
    6. [Calculate correlation and regression](https://github.com/alyssahondrade/matplotlib-challenge/blob/main/README.md#calculate-correlation-and-regression)
3. [References](https://github.com/alyssahondrade/matplotlib-challenge/blob/main/README.md#references)

## Introduction
### Goal
A new pharmaceutical company that specialises in anti-cancer medications has recently started screening for potential treatments for Squamous Cell Carcinoma (SCC). A recent animal study of the tumor development of 249 mice over 45 days has been generated to compare the performance of a few drugs of interest against the company's drug of interest, Capomulin.

The goal of the project is to create a top-level summary of the results, with corresponding tables and figures, that compares the performance of Capomulin against other drugs of interest.

The project is broken down to the following tasks:
1. Prepare the data
2. Generate summary statistics
3. Create bar and pie charts
4. Calculate quartiles, find outliers, and create a box plot
5. Create a line and scatter plot
6. Calculate correlation and regression

### Repository Structure
The Jupyter notebook [`pymaceuticals.ipynb`](https://github.com/alyssahondrade/matplotlib-challenge/blob/main/pymaceuticals.ipynb) is contained in the root directory.

`Resources` directory contains the datasets: [`Mouse_metadata.csv`](https://github.com/alyssahondrade/matplotlib-challenge/blob/main/Resources/Mouse_metadata.csv) and [`Study_results.csv`](https://github.com/alyssahondrade/matplotlib-challenge/blob/main/Resources/Study_results.csv)

### Dataset
The datasets were generated by **Mockaroo, LLC (2022) Realistic Data Generator**.

## Approach
### Prepare the data
1. Understand the contents of each dataset:
    - [`Mouse_metadata.csv'`](https://github.com/alyssahondrade/matplotlib-challenge/blob/main/Resources/Mouse_metadata.csv) contained `249` rows with columns: `['Mouse ID', 'Drug Regimen', 'Sex', 'Age_months', 'Weight (g)']`.
    - [`Study_results.csv`](https://github.com/alyssahondrade/matplotlib-challenge/blob/main/Resources/Study_results.csv) contained `1893` rows with columns: `['Mouse ID', 'Timepoint', 'Tumor Volume (mm3)', 'Metastatic sites']`.
2. Merge the dataset, using `pd.merge()`, and identify duplicates, using Pandas `DataFrame.duplicated()`.
3. Remove mice with duplicated values, confirming the number by identifying unique `Mouse ID`, and create a cleaned DataFrame.

### Generate summary statistics
1. For each drug regimen, calculate the following statistcs: `mean`, `median`, `variance`, `standard deviation`, and `SEM` of the tumor volume.
2. Two methods that can be used:
    - Use `groupby()` for each statistic.
    - Use the aggregation method `agg()` using a single line of code.

### Create bar and pie charts
1. Create two bar charts using: Pandas `DataFrame.plot()` method, and Matplotlib's `pyplot` method.
    - Sort the values prior to plotting, with the highest number of observed timepoints first.
    - Add an appropriate title and labels to each plot.
2. Create two pie charts using: Pandas `DataFrame.plot()` method, and Matplotlib's `pyplot` method.
    - Sort the values prior to plotting to ensure the resulting plot matches the expected figure.
    - Add a label and annotate the percentage value in the correct pie slice.

### Calculate quartiles, find outliers, and create a box plot
1. Create a list of the four drug regimens of interest: `['Capomulin', 'Ramicane', 'Infubinol', 'Ceftamin']`.
2. Using a for-loop over the four treatments, isolate the data for each drug and append to the `tumor_data` list.
3. Within the for-loop, calculate the following:
    - Lower quartile, using `quantile(0.25)`
    - Upper quartile, using `quantile(0.75)`
    - Inter-quartile range (IQR), using `upper_quartile - lower_quartile`
    - Lower bounds, using `lower_quartile - (1.5*iqr)`
    - Upper bounds, using `upper_quartile + (1.5*iqr)`
4. Identify outliers using the calculated upper and lower bounds.
5. Display the IQR and outliers for each treatment group.

### Create a line and scatter plot
1. Line plot - Single mouse:
    - For a single mouse, isolate the `Tumor Volume (mm3)` and `Timepoint`.
    - Use the retrieved data to create a line plot.
2. Scatter plot - Capomulin regimen average tumor volume vs mouse weight:
    - For the `Capomulin` regimen, isolate `Mouse ID`, `Tumor Volume (mm3)`, and `Weight (g)`.
    - Use `groupby().mean()` over the retrieved data.
    - Use the derived data to create a scatter plot.

### Calculate correlation and regression
1. Correlation Coefficient
    - Use `st.pearsonr()` to calculate the correlation coefficient between the `groupby().mean()` DataFrame's `Weight (g)` and `Tumor Volume (mm3)`.
    - Print the result, rounded to 2 decimal places for readability.
2. Linear Regression Model
    - Use the `linregress()` function to calculate the regression attributes: `slope`, `intercept`, `rvalue`, `pvalue`, `stderr`.
    - Use the attributes to get the regression values using the slope equation: `x_values * slope + intercept`.
    - Overlay the regression line on the Capomulin regimen scatter plot.

## References
The statistics linear regression equation is derived from the Bootcamp Week 5 Day 3.

- [1] Pandas Aggregate Rows [https://stackoverflow.com/questions/41581044/pandas-aggregate-rows-for-a-given-column-and-count-the-number](https://stackoverflow.com/questions/41581044/pandas-aggregate-rows-for-a-given-column-and-count-the-number)

- [2] Modify Pandas Boxplot Output [https://saturncloud.io/blog/how-to-modify-pandas-boxplot-output/](https://saturncloud.io/blog/how-to-modify-pandas-boxplot-output/)

- [3] Chages to Default Style [https://matplotlib.org/stable/users/prev_whats_new/dflt_style_changes.html](https://matplotlib.org/stable/users/prev_whats_new/dflt_style_changes.html)

- [4] How to Change Outlier Point Symbol [https://stackoverflow.com/questions/65648502/how-to-change-outlier-point-symbol-in-python-matplotlib-pyplot](https://stackoverflow.com/questions/65648502/how-to-change-outlier-point-symbol-in-python-matplotlib-pyplot)

- [5] Matplotlib Boxplots [https://matplotlib.org/stable/gallery/statistics/boxplot_demo.html](https://matplotlib.org/stable/gallery/statistics/boxplot_demo.html)
