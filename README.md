# 🍽️ DineSight – SQL Project  

## 📌 Project Overview  
DineSight is a **SQL-powered analytics system** for restaurant reviews, orders, and social media engagement.  
It simulates how restaurants track customer behavior, ratings, and marketing impact through relational databases.  

---

## 🛠️ Tools & Technologies  
- SQL (MySQL / PostgreSQL)  
- ER Modeling (Lucidchart / Draw.io)  
- Data Analytics  

---

## 📂 Database Schema  

```sql
-- Restaurants table
CREATE TABLE restaurants (
    restaurant_id INT PRIMARY KEY,
    restaurant_name VARCHAR(100) NOT NULL,
    location VARCHAR(100),
    cuisine_type VARCHAR(50)
);

-- Customers table
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    customer_name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE,
    join_date DATE
);

-- Orders table
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    restaurant_id INT,
    order_date DATE,
    amount DECIMAL(10,2),
    FOREIGN KEY (customer_id) REFERENCES customers(customer_id),
    FOREIGN KEY (restaurant_id) REFERENCES restaurants(restaurant_id)
);

-- Reviews table
CREATE TABLE reviews (
    review_id INT PRIMARY KEY,
    customer_id INT,
    restaurant_id INT,
    rating INT CHECK(rating BETWEEN 1 AND 5),
    review_text TEXT,
    review_date DATE,
    FOREIGN KEY (customer_id) REFERENCES customers(customer_id),
    FOREIGN KEY (restaurant_id) REFERENCES restaurants(restaurant_id)
);

-- Social Media table
CREATE TABLE social_media (
    post_id INT PRIMARY KEY,
    restaurant_id INT,
    likes INT DEFAULT 0,
    comments INT DEFAULT 0,
    shares INT DEFAULT 0,
    post_date DATE,
    FOREIGN KEY (restaurant_id) REFERENCES restaurants(restaurant_id)
);
## 📥 Sample Data Inserts  

```sql
-- Restaurants
INSERT INTO restaurants VALUES
(1, 'SpiceHub', 'Dallas, TX', 'Indian'),
(2, 'BurgerTown', 'Austin, TX', 'Fast Food'),
(3, 'PastaFiesta', 'Houston, TX', 'Italian'),
(4, 'SushiZen', 'Plano, TX', 'Japanese'),
(5, 'TacoStreet', 'San Antonio, TX', 'Mexican');

-- Customers
INSERT INTO customers VALUES
(1, 'Alice Johnson', 'alice@example.com', '2024-01-10'),
(2, 'Bob Smith', 'bob@example.com', '2024-02-15'),
(3, 'Charlie Lee', 'charlie@example.com', '2024-03-20'),
(4, 'Diana Patel', 'diana@example.com', '2024-04-05'),
(5, 'Ethan Clark', 'ethan@example.com', '2024-05-25');

-- Orders
INSERT INTO orders VALUES
(1, 1, 1, '2024-06-01', 45.50),
(2, 2, 2, '2024-06-03', 18.75),
(3, 3, 3, '2024-06-05', 29.99),
(4, 4, 4, '2024-06-07', 52.40),
(5, 5, 5, '2024-06-09', 22.30);

-- Reviews
INSERT INTO reviews VALUES
(1, 1, 1, 5, 'Amazing food and great service!', '2024-06-01'),
(2, 2, 2, 4, 'Good burgers but a bit slow.', '2024-06-03'),
(3, 3, 3, 3, 'Average experience.', '2024-06-05'),
(4, 4, 4, 5, 'Best sushi I ever had!', '2024-06-07'),
(5, 5, 5, 4, 'Tacos were fresh and tasty.', '2024-06-09');

-- Social Media
INSERT INTO social_media VALUES
(1, 1, 120, 15, 10, '2024-06-01'),
(2, 2, 200, 25, 30, '2024-06-03'),
(3, 3, 80, 10, 5, '2024-06-05'),
(4, 4, 300, 50, 40, '2024-06-07'),
(5, 5, 150, 20, 15, '2024-06-09');

#### Top Restaurants by Number of Reviews  
SELECT r.restaurant_name, COUNT(rv.review_id) AS total_reviews
FROM reviews rv
JOIN restaurants r ON rv.restaurant_id = r.restaurant_id
GROUP BY r.restaurant_name
ORDER BY total_reviews DESC
LIMIT 5;

####Average Ratings per Restaurant
SELECT r.restaurant_name, ROUND(AVG(rv.rating),2) AS avg_rating
FROM reviews rv
JOIN restaurants r ON rv.restaurant_id = r.restaurant_id
GROUP BY r.restaurant_name
ORDER BY avg_rating DESC;

####Social Media Engagement Analysis
SELECT r.restaurant_name, 
       SUM(sm.likes) AS total_likes, 
       SUM(sm.comments) AS total_comments, 
       SUM(sm.shares) AS total_shares
FROM social_media sm
JOIN restaurants r ON sm.restaurant_id = r.restaurant_id
GROUP BY r.restaurant_name
ORDER BY total_likes DESC;

####Highest Spending Customers
SELECT c.customer_name, SUM(o.amount) AS total_spent
FROM orders o
JOIN customers c ON o.customer_id = c.customer_id
GROUP BY c.customer_name
ORDER BY total_spent DESC
LIMIT 5;

####Restaurants with Average Rating Above 4
SELECT r.restaurant_name, AVG(rv.rating) AS avg_rating
FROM reviews rv
JOIN restaurants r ON rv.restaurant_id = r.restaurant_id
GROUP BY r.restaurant_name
HAVING AVG(rv.rating) > 4;

## 🚀 Key Insights  
✔️ Identified top-performing restaurants by reviews and ratings  
✔️ Customer engagement tracked through likes, comments, and shares  
✔️ Found highest-spending customers for loyalty programs  
✔️ Filtered restaurants with consistently excellent ratings  

---

## 📈 Future Scope  
- Build interactive dashboards with Tableau/Power BI for visualization  
- Expand dataset across multiple cities and cuisines  
- Apply machine learning models to predict customer churn and sentiment  

---

## 🧑‍💻 Author  
**Aditya Shibe**  
📍 MS in Business Analytics & AI, University of Texas at Dallas  
🔗 [LinkedIn](www.linkedin.com/in/adityashibe) 
