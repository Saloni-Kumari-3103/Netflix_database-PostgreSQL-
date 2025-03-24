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
1️⃣ Count the number of Movies vs TV Shows

SELECT type, COUNT(*) AS total 
FROM netflix 
GROUP BY type;

2️⃣ List all movies released in a specific year (e.g., 2020)

SELECT title, release_year 
FROM netflix 
WHERE release_year = 2020;

3️⃣ Find the top 5 countries with the most content on Netflix

SELECT * FROM (
    SELECT UNNEST(STRING_TO_ARRAY(country, ',')) AS country,
           COUNT(*) AS total_content
    FROM netflix
    GROUP BY 1
) AS t1
WHERE country IS NOT NULL
ORDER BY total_content DESC
LIMIT 5;

4️⃣ Identify the longest movie

SELECT *
FROM netflix
WHERE type = 'Movie' AND duration IS NOT NULL
ORDER BY SPLIT_PART(duration, ' ', 1)::INT DESC
LIMIT 1;

5️⃣ Find content added in the last 5 years

SELECT *
FROM netflix
WHERE TO_DATE(date_added, 'Month DD, YYYY') >= CURRENT_DATE - INTERVAL '5 years';

6️⃣ Find all the movies/TV shows by director 'Rajiv Chilaka'

SELECT *
FROM (
    SELECT *, UNNEST(STRING_TO_ARRAY(director, ',')) AS director_name
    FROM netflix
) AS t
WHERE director_name = 'Rajiv Chilaka';

7️⃣ List all TV shows with more than 5 seasons

SELECT *
FROM netflix
WHERE type = 'TV Show'
  AND SPLIT_PART(duration, ' ', 1)::INT > 5;

8️⃣ Count the number of content items in each genre

SELECT UNNEST(STRING_TO_ARRAY(listed_in, ',')) AS genre,
       COUNT(*) AS total_content
FROM netflix
GROUP BY 1;

9️⃣ Find top 5 years with highest average content release in India

SELECT country, release_year, COUNT(show_id) AS total_release,
       ROUND(COUNT(show_id)::NUMERIC / (SELECT COUNT(show_id) FROM netflix WHERE country = 'India')::NUMERIC * 100, 2) AS avg_release
FROM netflix
WHERE country = 'India'
GROUP BY country, release_year
ORDER BY avg_release DESC
LIMIT 5;

🔟 List all movies that are documentaries

SELECT * FROM netflix
WHERE listed_in LIKE '%Documentaries';

1️⃣1️⃣ Find all content without a director

SELECT * FROM netflix
WHERE director IS NULL;

1️⃣2️⃣ Find how many movies actor 'Salman Khan' appeared in the last 10 years

SELECT * FROM netflix
WHERE casts LIKE '%Salman Khan%'
  AND release_year > EXTRACT(YEAR FROM CURRENT_DATE) - 10;

1️⃣3️⃣ Find the top 10 actors with the most movie appearances in India

SELECT UNNEST(STRING_TO_ARRAY(casts, ',')) AS actor,
       COUNT(*)
FROM netflix
WHERE country = 'India'
GROUP BY actor
ORDER BY COUNT(*) DESC
LIMIT 10;

1️⃣4️⃣ Categorize content as 'Good' or 'Bad' based on keywords in description

SELECT category, COUNT(*) AS content_count
FROM (
    SELECT CASE 
             WHEN description ILIKE '%kill%' OR description ILIKE '%violence%' THEN 'Bad'
             ELSE 'Good'
         END AS category
    FROM netflix
) AS categorized_content
GROUP BY category;

🛠 How to Use

Import the Netflix dataset into a PostgreSQL database.

Run the SQL queries in your database client.

Analyze the results to gain insights into Netflix's content.

🏗 Technologies Used

PostgreSQL

SQL

👤 Author

[Your Name]

📜 License

This project is licensed under the MIT License.
