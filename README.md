# 🎬 Netflix Movies and TV Shows Data Analysis using SQL

![Netflix Logo](logo.png)

## 📌 Overview

This project involves a comprehensive analysis of Netflix's movies and TV shows data using SQL. The goal is to extract valuable insights and answer various business questions based on the dataset.

---
## 🎯 Objectives

- 📊 Analyze the distribution of content types (Movies vs. TV Shows).
- 🎭 Identify the most common ratings for movies and TV shows.
- 🌍 List and analyze content based on release years, countries, and durations.
- 🔍 Explore and categorize content based on specific criteria and keywords.

---
## 📂 Dataset

📥 **Source**: The data for this project is sourced from Kaggle.

🔗 **Dataset Link:** [Movies Dataset](https://www.kaggle.com/datasets/shivamb/netflix-shows?resource=download)

---
## 📑 Schema

```sql
DROP TABLE IF EXISTS netflix;
CREATE TABLE netflix (
    show_id      VARCHAR(5),
    type         VARCHAR(10),
    title        VARCHAR(250),
    director     VARCHAR(550),
    casts        VARCHAR(1050),
    country      VARCHAR(550),
    date_added   VARCHAR(55),
    release_year INT,
    rating       VARCHAR(15),
    duration     VARCHAR(15),
    listed_in    VARCHAR(250),
    description  VARCHAR(550)
);
```

---
## 🔥 Business Problems and SQL Solutions

### 1️⃣ 🎥 Count the Number of Movies vs. TV Shows
```sql
SELECT type, COUNT(*) FROM netflix GROUP BY 1;
```
**Objective:** Determine the distribution of content types on Netflix.

---

### 2️⃣ ⭐ Find the Most Common Rating for Movies and TV Shows
```sql
WITH RatingCounts AS (
    SELECT type, rating, COUNT(*) AS rating_count
    FROM netflix
    GROUP BY type, rating
),
RankedRatings AS (
    SELECT type, rating, rating_count,
           RANK() OVER (PARTITION BY type ORDER BY rating_count DESC) AS rank
    FROM RatingCounts
)
SELECT type, rating AS most_frequent_rating
FROM RankedRatings WHERE rank = 1;
```
**Objective:** Identify the most frequently occurring rating for each type of content.

---

### 3️⃣ 📅 List All Movies Released in 2020
```sql
SELECT * FROM netflix WHERE release_year = 2020;
```
**Objective:** Retrieve all movies released in a specific year.

---

### 4️⃣ 🌎 Find the Top 5 Countries with the Most Content on Netflix
```sql
SELECT country, COUNT(*) AS total_content
FROM netflix
WHERE country IS NOT NULL
GROUP BY country
ORDER BY total_content DESC
LIMIT 5;
```
**Objective:** Identify the top 5 countries with the highest number of content items.

---

### 5️⃣ ⏳ Identify the Longest Movie
```sql
SELECT * FROM netflix
WHERE type = 'Movie'
ORDER BY SPLIT_PART(duration, ' ', 1)::INT DESC;
```
**Objective:** Find the movie with the longest duration.

---

### 6️⃣ 🆕 Find Content Added in the Last 5 Years
```sql
SELECT * FROM netflix
WHERE TO_DATE(date_added, 'Month DD, YYYY') >= CURRENT_DATE - INTERVAL '5 years';
```
**Objective:** Retrieve content added to Netflix in the last 5 years.

---

### 7️⃣ 🎬 Find All Movies/TV Shows by Director 'Rajiv Chilaka'
```sql
SELECT * FROM netflix WHERE director LIKE '%Rajiv Chilaka%';
```
**Objective:** List all content directed by 'Rajiv Chilaka'.

---

### 8️⃣ 📺 List All TV Shows with More Than 5 Seasons
```sql
SELECT * FROM netflix WHERE type = 'TV Show' AND SPLIT_PART(duration, ' ', 1)::INT > 5;
```
**Objective:** Identify TV shows with more than 5 seasons.

---

### 9️⃣ 🎭 Count the Number of Content Items in Each Genre
```sql
SELECT listed_in AS genre, COUNT(*) AS total_content FROM netflix GROUP BY 1;
```
**Objective:** Count the number of content items in each genre.

---

### 🔟 🇮🇳 Find Top 5 Years with Highest Avg. Content Release in India
```sql
SELECT release_year, COUNT(show_id) AS total_release
FROM netflix
WHERE country = 'India'
GROUP BY release_year
ORDER BY total_release DESC
LIMIT 5;
```
**Objective:** Identify the years with the highest content release in India.

---
## 🏆 Findings and Conclusion

- 🎬 **Content Distribution:** The dataset contains a diverse range of movies and TV shows with varying ratings and genres.
- 🌟 **Common Ratings:** Insights into the most common ratings provide an understanding of the content's target audience.
- 🌍 **Geographical Insights:** The top countries and the average content releases by India highlight regional content distribution.
- 🧐 **Content Categorization:** Categorizing content based on specific keywords helps in understanding the nature of content available on Netflix.

This analysis provides a comprehensive view of Netflix's content and can help inform content strategy and decision-making.

---
## 👨‍💻 Author - Brian Achaye "The Data Whisperer"

This project is part of my portfolio, showcasing SQL skills essential for data analysis roles. Feel free to reach out with any questions or collaboration requests!

### 🌟 Stay Updated and Join the Community!

💡 **For more content on SQL, data analysis, and insights, follow me:**

- 🌍 **Website**: [Visit my website](https://brianachaye.com/)
- 🎥 **YouTube**: [Subscribe for tutorials](https://www.youtube.com/@brianachaye)
- 📸 **TikTok**: [Follow for daily tips](https://www.tiktok.com/@brianachaye)
- 💼 **LinkedIn**: [Connect with me professionally](https://www.linkedin.com/in/BrianAchaye)

🚀 *Thank you for your support, and I look forward to connecting with you!*