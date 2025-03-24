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
```
# 📊 Netflix Data Analysis Using SQL

## 📌 Overview

This project contains various SQL queries to analyze the Netflix dataset. The queries cover content categorization, director analysis, country-based trends, and more. This analysis helps understand Netflix's content distribution, trends, and patterns.

## 📂 Dataset Description

The dataset includes the following columns:

- **show\_id**: Unique ID for each show
- **type**: Movie or TV Show
- **title**: Title of the show
- **director**: Director of the show
- **casts**: Actors involved in the show
- **country**: Country where the show was produced
- **date\_added**: Date when the show was added to Netflix
- **release\_year**: Year of release
- **duration**: Duration of the content (minutes or seasons for TV shows)
- **listed\_in**: Genre/categories of the show
- **description**: Brief description of the show

## 🚀 SQL Queries

### 🎥 1. Count of Movies vs TV Shows
```sql
SELECT type, COUNT(*) AS total FROM netflix GROUP BY type;
```

### 📅 2. List all movies released in a specific year (e.g., 2020)
```sql
SELECT title, release_year FROM netflix WHERE release_year = 2020;
```

### 🌍 3. Find the top 5 countries with the most content on Netflix
```sql
SELECT country, COUNT(*) AS total_content FROM netflix WHERE country IS NOT NULL GROUP BY country ORDER BY total_content DESC LIMIT 5;
```

### 🎬 4. Identify the longest movie
```sql
SELECT * FROM netflix WHERE type = 'Movie' AND duration IS NOT NULL ORDER BY SPLIT_PART(duration, ' ', 1)::INT DESC LIMIT 1;
```

### ⏳ 5. Find content added in the last 5 years
```sql
SELECT * FROM netflix WHERE TO_DATE(date_added, 'Month DD, YYYY') >= CURRENT_DATE - INTERVAL '5 years';
```

### 🎭 6. Find all the movies/TV shows by director 'Rajiv Chilaka'
```sql
SELECT * FROM netflix WHERE director LIKE '%Rajiv Chilaka%';
```

### 📺 7. List all TV shows with more than 5 seasons
```sql
SELECT * FROM netflix WHERE type = 'TV Show' AND SPLIT_PART(duration, ' ', 1)::INT > 5;
```

### 🎭 8. Count the number of content items in each genre
```sql
SELECT UNNEST(STRING_TO_ARRAY(listed_in, ',')) AS genre, COUNT(*) AS total_content FROM netflix GROUP BY 1;
```

### 🇮🇳 9. Find top 5 years with highest average content release in India
```sql
SELECT release_year, COUNT(show_id) AS total_release FROM netflix WHERE country = 'India' GROUP BY release_year ORDER BY total_release DESC LIMIT 5;
```

### 🎥 10. List all movies that are documentaries
```sql
SELECT * FROM netflix WHERE listed_in LIKE '%Documentaries%';
```



⭐ **If you find this project helpful, don't forget to give it a star!** ⭐



🛠 How to Use

Import the Netflix dataset into a PostgreSQL database.

Run the SQL queries in your database client.

Analyze the results to gain insights into Netflix's content.

🏗 Technologies Used

PostgreSQL

SQL

👤 Author

[SALONI KUMARI]


