# 🏠 Airbnb NYC Analysis  

## 📌 Project Overview  
This project analyzes Airbnb listings in New York City using **SQL & Power BI** to uncover insights into pricing trends, availability, and demand.  

## 📊 Tools & Technologies Used  
- **SQL (PostgreSQL / MySQL)** – Data cleaning, transformation, and analysis  
- **Power BI** – Interactive visualizations and dashboards  
- **Excel / CSV** – Data preprocessing and initial exploration  

## 🔍 Key Business Insights  
✅ **Pricing Trends:** Manhattan has the highest average rental prices, while Brooklyn offers more affordable options.  
✅ **Availability:** Listings in Brooklyn have higher availability compared to Manhattan and Queens.  
✅ **Preferred Room Types:** Entire homes/apartments are the most listed and booked properties.  
✅ **Demand Analysis:** Areas near tourist attractions tend to have higher demand and pricing.  

## 📊 Power BI Dashboard & Visuals  
Below are some key visualizations from the **Power BI dashboard**:  

![Airbnb Listings & Availability](https://github.com/Chaitra1609/Airbnb-NYC-Analysis/blob/main/Airbnb%20Listings%20&%20Availability%20Across%20NYC.png?raw=true)  
*Figure: Distribution of Airbnb listings across different boroughs in NYC. The bubble size represents the average availability of listings, while colors indicate different room types.*  

![Average Price Map](https://github.com/Chaitra1609/Airbnb-NYC-Analysis/blob/main/Average%20Price%20by%20Neighborhood%20Group%20&%20Room%20Type.png?raw=true)  
*Figure: Geographic distribution of listings and their average price across NYC. The visualization highlights price variations by room type and neighborhood group.*  
  

## 📂 Dataset Information  
- **Source:** Inside Airbnb ([http://insideairbnb.com/](http://insideairbnb.com/))  
- **Data Used:**  
  - Listing details (price, room type, availability, number of reviews)  
  - Location-based insights (borough-wise distribution)  
  - Host and property details  

## \ud83d\udcc8 SQL Queries Used  
Below are some of the key SQL queries used in this project:  

### 1. Find the Most Popular Hosts with the Highest Number of Listings  
```sql
SELECT host_id, host_name, COUNT(*) AS total_listings
FROM airbnb_listings
GROUP BY host_id, host_name
ORDER BY total_listings DESC
LIMIT 10;
```

### 2. Average Price per Neighborhood  
```sql
SELECT neighbourhood, AVG(price) AS avg_price
FROM airbnb_listings
GROUP BY neighbourhood
ORDER BY avg_price DESC;
```

### 3. Top-Rated Listings Using RANK() Function  
```sql
SELECT listing_id, name, neighbourhood, avg_rating,
       RANK() OVER (PARTITION BY neighbourhood ORDER BY avg_rating DESC) AS rank
FROM airbnb_listings
WHERE avg_rating IS NOT NULL;
```

### 4. Total Reviews per Borough  
```sql
SELECT neighbourhood_group, SUM(number_of_reviews) AS total_reviews
FROM airbnb_listings
GROUP BY neighbourhood_group
ORDER BY total_reviews DESC;
```

### 5. Listings Count by Room Type  
```sql
SELECT room_type, COUNT(*) AS listing_count
FROM airbnb_listings
GROUP BY room_type
ORDER BY listing_count DESC;
```

### 6. Filter Listings with Non-Null Ratings  
```sql
SELECT *
FROM airbnb_listings
WHERE avg_rating IS NOT NULL;
```

### 7. Find the Top 5 Highest Revenue-Generating Listings  
(Assuming revenue = price * number_of_reviews)
```sql
SELECT listing_id, name, host_name, price, number_of_reviews, (price * number_of_reviews) AS revenue
FROM airbnb_listings
ORDER BY revenue DESC
LIMIT 5;
```

