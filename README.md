# 📊 Upwork Freelancer Performance Analytics

## 📁 Overview

This project analyzes global freelancer data from an Upwork-style platform. It explores hourly rates, 
satisfaction scores, skill trends, and regional activity using Tableau for visualization and Python (Pandas) for preprocessing.

The goal is to uncover trends in performance, identify top-paying skills and regions,
and provide data-driven insights for clients and freelancers alike.

---

## 🎯 Objective

- Understand trends in hourly rates by skill and experience
- Compare freelancer activity across countries and genders
- Analyze client satisfaction and ratings by region and skill
- Create an interactive dashboard for insights using Tableau

---

## 🧹 Data Cleaning (Python)

Data was cleaned using a custom Python script to ensure consistency before visualizing in Tableau. Steps included:

- Removed special characters from `name`
- Standardized `gender`, `is_active`, and `client_satisfaction`
- Converted `hourly_rate` from string to numeric by removing `$` and `USD`
- Handled missing and invalid entries in `rating`

```python
import pandas as pd

df = pd.read_csv('global_freelancers_raw.csv')

# Clean client satisfaction
df['client_satisfaction'] = df['client_satisfaction'].astype(str).str.strip().str.replace('%', '', regex=False)
df['client_satisfaction'] = df['client_satisfaction'].str.replace('nan', '')

# Clean gender
df['gender'] = df['gender'].astype(str).str.strip().str.lower()
df['gender'] = df['gender'].map({'m': 'Male', 'male': 'Male', 'f': 'Female', 'female': 'Female'})

# Clean name
df['name'] = df['name'].str.strip('123._')

# Clean hourly rate
df['hourly_rate (USD)'] = df['hourly_rate (USD)'].astype(str).str.replace('$', '', regex=False)
df['hourly_rate (USD)'] = df['hourly_rate (USD)'].str.replace('USD', '', regex=False).str.strip()

# Clean rating
df['rating'] = df['rating'].apply(lambda x: "" if pd.isna(x) or x == 0.0 else x)

# Clean is_active
df['is_active'] = df['is_active'].astype(str).str.strip().str.lower()
df['is_active'] = df['is_active'].replace({
    '1': 'Yes', 'y': 'Yes', 'yes': 'Yes', 'true': 'Yes',
    '0': 'No', 'n': 'No', 'no': 'No', 'false': 'No'
})

df.to_csv('new_cleaned_data.csv', index=False)


## 📊 Dashboard Highlights

### Key Sections:
- 🌍 **Freelancer Count by Country**
- 💼 **Top Skills by Hourly Rate**
- 💲 **Experience vs Hourly Rate**
- 📊 **Ratings by Region & Skill (Heatmap)**
- 👥 **Gender and Age Distribution**
- 📈 **Client Satisfaction Overview**
- 📌 **Active vs Inactive Freelancers**

---

## 🔍 Key Insights

- **Avg Hourly Rate**: `$52.46`
- **Active Freelancers**: `44.6%`
- **Top Skills**: Blockchain, Web Development, Cybersecurity
- **Top Region by Ratings**: UI/UX in Asia
- **Most Profitable Experience Level**: 13 years
- **Client Satisfaction Avg**: 79.27%

---

## 🛠️ Tools & Technologies

- **Tableau Public** – for dashboard design and data visualization  
- **Python (Pandas)** – for data cleaning and preprocessing  
- **CSV** – source data format  

---

## 🗂️ Project Structure
📦 upwork-freelancer-analytics
├── 📄 global_freelancers_raw.csv       # Raw dataset
├── 🧹 data_cleaning.py                 # Python script for cleaning
├── 📊 Screenshot-2025-08-01.png        # Dashboard preview image
└── 📘 README.md                        # This documentation


---

## 🚀 Live Dashboard

📌 [🔗 View on Tableau Public](#)  
> *(Replace this link with your Tableau Public link)*

---

## ✅ Conclusion

This project provides a complete overview of freelancer performance using real-world-style data. By combining data wrangling in
Python and powerful visuals in Tableau, the analysis delivers insights into pricing trends, in-demand skills, satisfaction levels,
and regional strengths to support freelance market decision-making.
