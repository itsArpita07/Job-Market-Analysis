# 📊 Data Analyst Job Market Analysis in the US

## 🔍 Overview

Welcome to my analysis of the data job market, with a specific focus on **Data Analyst** roles. This project emerged from a personal goal to better understand and navigate the job landscape. It examines in-demand and high-paying skills to uncover optimal career opportunities for data analysts.

The dataset was sourced from **Luke Barousse's Python Course**, offering detailed insights into job titles, salaries, locations, and required skills. Using Python, I’ve explored questions like:

- Which skills are most in demand?
- What are the latest trends for Data Analysts?
- How do skills relate to salary?
- Which skills strike a balance between high demand and high pay?

---

## ❓ Key Questions

1. What are the most in-demand skills for the top 3 data job roles?
2. How are in-demand skills trending for Data Analysts?
3. How well do jobs and skills pay for Data Analysts?
4. How do average salaries for Data Analysts vary by work setting?

---

## 🛠 Tools Used


- 🐍 **Python** – Core language for data analysis  
- 🐼 **Pandas** – Data wrangling and preprocessing  
- 📊 **Matplotlib** – Basic data visualizations  
- 🎨 **Seaborn** – Advanced and aesthetic visualizations  
- 📓 **Jupyter Notebook** – Exploratory analysis and prototyping  
- 💻 **VS Code** – Script development and editing  
- 🔧 **Git** & 🌐 **GitHub** – Version control and project sharing

---

## 🧹 Data Preparation and Cleanup

This section details the process of preparing the dataset for analysis, focusing on improving accuracy, consistency, and usability.

### 📥 Importing & Cleaning the Data

The workflow begins with importing the required libraries and loading the dataset. Initial cleaning steps are then performed to address missing values, correct data types, and remove inconsistencies to ensure high-quality data for analysis.

```python
import pandas as pd
import numpy as np
import seaborn as sns
import ast
import matplotlib.pyplot as plt
from datasets import load_dataset

# Load dataset
dataset = load_dataset('lukebarousse/data_jobs')
df = dataset['train'].to_pandas()

# Convert date column to datetime format
df['job_posted_date'] = pd.to_datetime(df['job_posted_date'])

# Parse skill strings into Python lists
df['job_skills'] = df['job_skills'].apply(lambda x: ast.literal_eval(x) if pd.notna(x) else x)
```
## 📊 The Analysis

Each Jupyter notebook in this project focuses on a specific aspect of the data job market, using targeted analysis and visualizations to uncover key trends.

## US Filter for U.S. Based Jobs

To focus the analysis specifically on the U.S. job market, the dataset is filtered to include only job listings located in the **United States**.

```python
df_DA_US = df[(df['job_title_short'] == 'Data Analyst') & (df['job_country'] == 'United States')]
```
## 🗺️ Top Locations for Data Analyst Roles in the U.S.

To identify regional demand, job postings were grouped by location. The top 10 U.S. cities with the highest number of job listings for Data Analysts were visualized.

### 📊 Python Visualization Code
```python
df_plot = df_DA_US['job_location'].value_counts().head(10).to_frame().reset_index()
df_plot.columns = ['job_location', 'count']

sns.barplot(data=df_plot, x='count', y='job_location', palette='viridis')
plt.title('Top 10 Job Locations for Data Analysts in the US')
plt.xlabel('Number of Job Postings')
plt.tight_layout()
plt.show()
```
## 🖼️ Results

### Top 10 Job Locations for Data Analysts in the U.S.

The following visualization displays the top 10 U.S. locations with the highest number of Data Analyst job postings.

![Top 10 Job Locations](https://github.com/itsArpita07/Data-Project/blob/main/Project/Images/output_1.png)


*Bar graph visualizing the number of job postings by location for Data Analysts in the U.S.*


## 🏢 Top 10 Companies for Data Analyst Roles in the U.S.

The following analysis visualizes the top 10 companies with the highest number of job postings for Data Analysts in the U.S.

### 📊 Python Visualization Code
```python
df_plot = df_DA_US['company_name'].value_counts().head(10).to_frame().reset_index()
df_plot.columns = ['company_name', 'count']

sns.barplot(data=df_plot, x='count', y='company_name', palette='viridis')
plt.title('Top 10 Companies for Data Analysts in the US')
plt.xlabel('Number of Job Postings')
plt.tight_layout()
plt.show()
```
## 🖼️ Results

### Top 10 Companies for Data Analysts in the U.S.

The following visualization displays the top 10 U.S. companies with the highest number of Data Analyst job postings.

![Top 10 Companies](https://github.com/itsArpita07/Data-Project/blob/main/Project/Images/output_2.png)

*Bar graph visualizing the number of job postings by company for Data Analysts in the U.S.*


## 1️⃣ What are the most in-demand skills for the top 3 data job roles?

To identify the most in-demand skills, the dataset was filtered to select the top 3 most common data job titles. The top 5 skills for each role were then extracted and analyzed.

This analysis highlights the most valued skills across roles, providing clear guidance on which skill sets are prioritized in the current job market.

📓 Detailed steps and visualizations can be found in the notebook: [`2_Skill_Demand.ipynb`](https://github.com/itsArpita07/Data-Project/blob/main/Project/2_Skill_demand.ipynb)

## 📊 Visualize Data

The following visualization displays the top 5 skills for each data job title, showcasing the skill count for each role.

### 📊 Python Visualization Code
```python
fig, ax = plt.subplots(len(job_titles), 1)
sns.set_theme(style="ticks")

for i, job_title in enumerate(job_titles):
    df_plot = df_skills_count[df_skills_count['job_title_short'] == job_title].head(5)
    sns.barplot(data=df_plot, x='skill_count', y='job_skills', ax=ax[i])
    ax[i].set_title(job_title)
    ax[i].set_xticks(range(0, 45001, 5000))
    ax[i].legend().set_visible(False)

fig.suptitle('Top 5 Skills for Each Job Title')
fig.tight_layout()
plt.show()
```

## 🖼️ Results

### Likelihood of Skills Requested in Job Postings

The following visualization displays the top 5 skills for each data job title, highlighting the skill count associated with each role.

![Top 5 Skills for Each Job Title](https://github.com/itsArpita07/Data-Project/blob/main/Project/Images/output_3.png)

*Bar graph visualizing the salary for the top 3 data roles and their top 5 skills associated with each.*

## 📝 Insights

- SQL is the most requested skill for both Data Analysts (50.8%) and Data Scientists (51.05%).
- Python is the top skill for Data Engineers, appearing in 68.3% of job postings.
- Data Engineers demand more specialized skills like AWS (42.81%), Azure (32.27%), and Spark (32.05%).
- Data Analysts and Data Scientists prioritize general tools like Excel (40.58%) and Tableau (Analysts: 28.48%, Scientists: 23.56%).
- Python is crucial across all roles, with strong demand in Data Scientists (72.04%) and Data Engineers (64.89%).


## 2️⃣ How Are In-Demand Skills Trending for Data Analysts?

To analyze the trend of in-demand skills for Data Analysts in 2023, data analyst positions were filtered, and the skills were grouped by the month of job postings. This approach helped identify the top 5 skills for Data Analysts by month, showing the changes in skill popularity throughout 2023.

View my notebook with detailed steps here: [3_Skills_Trend](https://github.com/itsArpita07/Data-Project/blob/main/Project/3_Skill_trend.ipynb)

## 📊 Visualize Data

The following line plot visualizes the trending top skills for Data Analysts in the U.S. throughout 2023, showing the likelihood of these skills appearing in job postings over time.

### 📊 Python Visualization Code
```python
from matplotlib.ticker import PercentFormatter

sns.lineplot(data=df_DA_US_percent.iloc[:, :5], dashes=False, palette='tab10')
plt.title('Trending Top Skills for Data Analysts in the US')
plt.ylabel('Likelihood in Job Posting')
plt.xlabel('2023')
plt.gca().yaxis.set_major_formatter(PercentFormatter(decimals=0))
plt.show()
```
## 🖼️ Results

### Trending Top Skills for Data Analysts in the U.S.
The following visualization displays the top trending skills for Data Analysts throughout 2023, showing the likelihood of these skills appearing in job postings over time.

![Trending Top Skills for Data Analysts](https://github.com/itsArpita07/Data-Project/blob/main/Project/Images/output_4.png)

*Line plot visualizing the trending top skills for Data Analysts in the U.S. throughout 2023.*
  