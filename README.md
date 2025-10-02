# zomato-db-case-study
A Zomato-db-case-study database in MySQL with synthetic data and analytical SQL queries for customer, restaurant, menu, delivery, and reviews insights.

# 🍽️ Zomato_DB - Food Delivery Database (MySQL)

A Zomato-style food delivery database built with **MySQL**.  
It simulates customers, restaurants, riders, orders, menu items, deliveries, and reviews with **synthetic data** (generated using Python Faker).  
The project also includes analytical SQL queries for **customer insights, restaurant performance, menu popularity, delivery efficiency, and rating analysis**.  

---

## 📂 Project Structure
- **Database**: ZOMATO_DB
- **Tables**:
  - `customers` – Customer details  
  - `restaurants` – Restaurant details  
  - `riders` – Delivery partners  
  - `orders` – Orders placed by customers  
  - `order_items` – Items included in each order  
  - `menu_items` – Menu offerings from restaurants  
  - `deliveries` – Delivery details & rider assignments  
  - `reviews` – Customer & rider feedback  

---

## ⚡ Features
- 10,000+ synthetic rows generated with Python **Faker**  
- Realistic Indian customer names, addresses, phone numbers  
- Randomized timestamps between **2020–2025**  
- Foreign key relationships for realistic constraints  
- 30+ sample SQL queries for analysis  

---

## 📊 Example Queries
## 1. Customer Analytics
#### Who are the top 10 customers by total spending?
B) Which customers placed more than 1 orders?
C) Which customers have ordered from multiple restaurants?
D) Which customer ordered the highest number of items overall?
E) What is the average order value per customer?

-- 2. Restaurant Performance
A) Which restaurant earned the most revenue?
B) Which are the top 3 restaurants by number of orders?
C) Which restaurant has the highest average order value?
D) Which restaurants have not received any orders?
E) Which restaurant has the highest number of unique customers?

-- 3. Menu Popularity
A) What is the most popular menu item across all restaurants?
B) Which restaurant’s menu item is the best-selling overall?
C) What are the top 5 most ordered items in 2025 ?
D) Which category of items (e.g., drinks, main course) is ordered the most?
D) Which items are frequently ordered together (combo analysis)?

-- 4. Delivery Efficiency
A) Which rider has completed the most deliveries?
B) What is the average delivery time per rider?
C) Which riders have more than 50 successful deliveries?
D) How many orders were cancelled due to delivery issues?
E) Which rider has the best average delivery time performance?

-- 5. Time-Based Insights
A) Which time slot (morning, afternoon, evening, night) has the most orders?
B) What is the busiest day of the week for orders?
C) What month in 2025 had the highest number of orders?
D) How do order volumes change between weekdays and weekends?
E) At what hour of the day are maximum orders placed?

-- 6. Rating & Review Analysis
A)  Which restaurant has the best average rating (with at least 10 reviews)?
B) Which rider has the highest average rating?
C) Which customers gave the most reviews?
D) What is the distribution of restaurant ratings (1–5 stars)?
E) What percentage of reviews include customer comments?



