# 🎬 Netflix Data Analysis with SQL

🚀 A collection of SQL queries to analyze Netflix's dataset, including content statistics, genres, directors, and country-wise trends.

## 📌 Table of Contents
- [Overview](#-overview)
- [Dataset Information](#-dataset-information)
- [Queries Included](#-queries-included)
- [Usage](#-usage)
- [Example Queries](#-example-queries)
- [Contributing](#-contributing)
- [Author](#-author)

---

## 📊 Overview
This repository contains **SQL queries** that help analyze Netflix content. You can:
✔ Find top genres and countries producing content  
✔ Identify top actors and directors  
✔ Filter content based on type, release year, or country  
✔ Categorize content based on keywords like `violence` and `kill`  

---

## 📂 Dataset Information
The dataset includes:
- **Columns:** `show_id`, `title`, `director`, `country`, `release_year`, `duration`, `listed_in`, `description`
- **Source:** Netflix dataset

---

## 📌 Queries Included

### 🎥 1. Count of Movies vs TV Shows
```sql
SELECT type, COUNT(*) AS total FROM netflix GROUP BY type;
