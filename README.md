# 🍽️ Zomato_DB - Food Delivery Database (MySQL)
A Zomato-style food delivery database built with **MySQL**.  
It simulates customers, restaurants, riders, orders, menu items, deliveries, and reviews with **synthetic data** (generated using Python Faker).  
The project also includes analytical SQL queries for **customer insights, restaurant performance, menu popularity, delivery efficiency, and rating analysis**.

# Project Overview
Project Title: zomato-db-case-study
Database: zomato_db

The zomato-db-case-study project is a relational database system built using MySQL that simulates an online food delivery platform like Zomato.
It manages data related to customers, restaurants, riders, orders, menu items, deliveries, and reviews.
The schema is carefully designed with foreign keys, constraints, and indexes to maintain data integrity and optimize query performance.
Synthetic data is generated using Python Faker, ensuring realistic Indian names, addresses, and phone numbers, with timestamps distributed between 2020–2025.
This provides a large dataset to explore customer behavior, restaurant performance, menu popularity, delivery efficiency, and review analysis.
The project includes over 30 analytical SQL queries, such as identifying top customers, calculating revenue per restaurant, analyzing delivery times, and finding the most popular menu items.

# Objective
The main objective of the zomato-db-case-study project is to design and implement a relational database named zomato_db that simulates an online food delivery platform.
It focuses on:
1. Efficiently managing data for customers, restaurants, riders, orders, and reviews.
2. Practicing SQL queries to analyze customer behavior, restaurant performance, and order insights.
3. Creating a realistic dataset using Faker for hands-on learning.
4. Building a foundation for data analytics and decision-making in the food delivery industry.

# Project Structure
## 1. Database setup
Database Creation:
The project begins by creating a database named zomato_db to store all data related to the food delivery platform.
Table Creation:
1. customers – stores customer details like name, phone number, email, city, address, and registration date.
2. restaurants – stores restaurant information including name, city, address, and operating hours.
3. riders – stores delivery partner details, signup date, rating, and active status.
4. orders – stores order information such as customer ID, restaurant ID, order datetime, status, total amount, and payment mode.
5. order_items – stores items in each order, including menu item ID, quantity, item price, and total price.
6. menu_items – stores menu details like item name, category, price, availability, and the restaurant it belongs to.
7. deliveries – stores delivery details including order ID, assigned rider, delivery status, pickup and delivery timestamps.
8. reviews – stores customer ratings and comments for both restaurants and riders.

```sql
CREATE DATABASE ZOMATO_DB;
USE ZOMATO_DB;

CREATE TABLE CUSTOMERS (
  CUSTOMER_ID INT AUTO_INCREMENT PRIMARY KEY,
  CUSTOMER_NAME VARCHAR(100) NOT NULL,
  PHONE VARCHAR(20) NOT NULL UNIQUE,
  EMAIL VARCHAR(50),
  CITY VARCHAR(50),
  ADDRESS TEXT,
  REG_DATE DATE
);

CREATE TABLE RESTAURANTS (
  RESTAURANT_ID INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  RESTAURANT_NAME VARCHAR(150) NOT NULL,
  CITY VARCHAR(50),
  ADDRESS TEXT,
  CUISINE_TYPE VARCHAR(100), -- Added
  OPENING_HOURS JSON,
  PHONE VARCHAR(20) UNIQUE
);

CREATE TABLE RIDERS (
  RIDER_ID INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  RIDER_NAME VARCHAR(100) NOT NULL,
  PHONE VARCHAR(20) UNIQUE, -- Recommended for contact
  SIGN_UP_DATE DATE,
  RATING DECIMAL(2,1) DEFAULT NULL CHECK (RATING BETWEEN 0.0 AND 5.0),
  IS_ACTIVE TINYINT(1) DEFAULT 1
);

CREATE TABLE ORDERS (
  ORDER_ID INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  CUSTOMER_ID INT UNSIGNED NOT NULL,
  RESTAURANT_ID INT UNSIGNED NOT NULL,
  ORDER_DATETIME TIMESTAMP DEFAULT CURRENT_TIMESTAMP, -- Changed DATETIME to TIMESTAMP
  ORDER_STATUS ENUM('PLACED', 'PREPARING', 'READY', 'OUT_FOR_DELIVERY', 'DELIVERED', 'CANCELLED') DEFAULT 'PLACED',
  TOTAL_AMOUNT DECIMAL(10,2) NOT NULL DEFAULT 0.00,
  PAYMENT_MODE ENUM('CASH', 'CARD', 'WALLET', 'UPI') DEFAULT 'CASH',
  FOREIGN KEY (CUSTOMER_ID) REFERENCES CUSTOMERS(CUSTOMER_ID) ON UPDATE CASCADE ON DELETE RESTRICT,
  FOREIGN KEY (RESTAURANT_ID) REFERENCES RESTAURANTS(RESTAURANT_ID) ON UPDATE CASCADE ON DELETE RESTRICT
);


CREATE TABLE DELIVERIES (
  DELIVERY_ID INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  ORDER_ID INT UNSIGNED UNIQUE NOT NULL,
  RIDER_ID INT UNSIGNED DEFAULT NULL,
  DELIVERY_STATUS ENUM('PENDING', 'ASSIGNED', 'OUT_FOR_DELIVERY', 'DELIVERED', 'CANCELLED') DEFAULT 'PENDING',
  PICKED_UP_AT DATETIME,
  DELIVERED_AT DATETIME,
  ESTIMATED_DELIVERY_TIME DATETIME,
  FOREIGN KEY (ORDER_ID) REFERENCES ORDERS(ORDER_ID) ON DELETE CASCADE ON UPDATE CASCADE,
  FOREIGN KEY (RIDER_ID) REFERENCES RIDERS(RIDER_ID) ON DELETE SET NULL ON UPDATE CASCADE
);

CREATE TABLE MENU_ITEMS (
  MENU_ITEM_ID INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  RESTAURANT_ID INT UNSIGNED NOT NULL,
  ITEM_NAME VARCHAR(150) NOT NULL,
  PRICE DECIMAL(8,2) NOT NULL CHECK (PRICE > 0),
  CATEGORY VARCHAR(50),
  IS_AVAILABLE TINYINT(1) DEFAULT 1,
  FOREIGN KEY (RESTAURANT_ID) REFERENCES RESTAURANTS(RESTAURANT_ID) ON DELETE CASCADE ON UPDATE CASCADE
);

CREATE TABLE ORDER_ITEMS (
  ORDER_ITEM_ID INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  ORDER_ID INT UNSIGNED NOT NULL,
  MENU_ITEM_ID INT UNSIGNED NOT NULL,
  QUANTITY INT UNSIGNED NOT NULL DEFAULT 1 CHECK (QUANTITY > 0),
  ITEM_PRICE DECIMAL(8,2) NOT NULL CHECK (ITEM_PRICE >= 0),
  TOTAL_PRICE DECIMAL(10,2) AS (QUANTITY * ITEM_PRICE) STORED,
  FOREIGN KEY (ORDER_ID) REFERENCES ORDERS(ORDER_ID) ON DELETE CASCADE ON UPDATE CASCADE,
  FOREIGN KEY (MENU_ITEM_ID) REFERENCES MENU_ITEMS(MENU_ITEM_ID) ON DELETE RESTRICT ON UPDATE CASCADE
);

CREATE TABLE REVIEWS (
  REVIEW_ID INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  CUSTOMER_ID INT UNSIGNED NOT NULL,
  RESTAURANT_ID INT UNSIGNED NOT NULL,
  RIDER_ID INT UNSIGNED, -- Now nullable: delivery may not have a rider
  RESTAURANT_RATING TINYINT UNSIGNED CHECK (RESTAURANT_RATING BETWEEN 1 AND 5),
  RIDER_RATING TINYINT UNSIGNED CHECK (RIDER_RATING BETWEEN 1 AND 5),
  COMMENT TEXT,
  CREATED_AT TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (CUSTOMER_ID) REFERENCES CUSTOMERS(CUSTOMER_ID) ON DELETE CASCADE ON UPDATE CASCADE,
  FOREIGN KEY (RESTAURANT_ID) REFERENCES RESTAURANTS(RESTAURANT_ID) ON DELETE CASCADE ON UPDATE CASCADE,
  FOREIGN KEY (RIDER_ID) REFERENCES RIDERS(RIDER_ID) ON DELETE CASCADE ON UPDATE CASCADE
);
```


## 📊 Example Queries
## 1. Customer Analytics
#### A) Who are the top 10 customers by total spending?
#### B) Which customers placed more than 1 orders?
#### C) Which customers have ordered from multiple restaurants?
#### D) Which customer ordered the highest number of items overall?
#### E) What is the average order value per customer?

## 2. Restaurant Performance
#### A) Which restaurant earned the most revenue?
```SELECT C.CUSTOMER_ID, C.CUSTOMER_NAME, SUM(TOTAL_AMOUNT) AS TOTAL_SPENDING FROM CUSTOMERS C 
INNER JOIN ORDERS O ON C.CUSTOMER_ID = O.CUSTOMER_ID
GROUP BY C.CUSTOMER_ID ORDER BY SUM(TOTAL_AMOUNT) DESC LIMIT 10;```

#### B) Which are the top 3 restaurants by number of orders?
#### C) Which restaurant has the highest average order value?
#### D) Which restaurants have not received any orders?
#### E) Which restaurant has the highest number of unique customers?

## 3. Menu Popularity
#### A) What is the most popular menu item across all restaurants?
#### B) Which restaurant’s menu item is the best-selling overall?
#### C) What are the top 5 most ordered items in 2025 ?
##### D) Which category of items (e.g., drinks, main course) is ordered the most?
#### E) Which items are frequently ordered together (combo analysis)?

## 4. Delivery Efficiency
#### A) Which rider has completed the most deliveries?
#### B) What is the average delivery time per rider?
#### C) Which riders have more than 50 successful deliveries?
#### D) How many orders were cancelled due to delivery issues?
#### E) Which rider has the best average delivery time performance?

## 5. Time-Based Insights
#### A) Which time slot (morning, afternoon, evening, night) has the most orders?
#### B) What is the busiest day of the week for orders?
#### C) What month in 2025 had the highest number of orders?
#### D) How do order volumes change between weekdays and weekends?
#### E) At what hour of the day are maximum orders placed?

## 6. Rating & Review Analysis
#### A)  Which restaurant has the best average rating (with at least 10 reviews)?
#### B) Which rider has the highest average rating?
#### C) Which customers gave the most reviews?
#### D) What is the distribution of restaurant ratings (1–5 stars)?
#### E) What percentage of reviews include customer comments?

# ✅ Conclusion
The zomato-db-case-study project demonstrates the design and implementation of a comprehensive MySQL relational database for an online food delivery platform.
It successfully captures all key entities, including customers, restaurants, orders, menu items, riders, deliveries, and reviews, while maintaining data integrity through foreign keys and constraints.Analysis of the dataset provides valuable insights into customer behavior, restaurant performance, menu popularity, delivery efficiency, and ratings.Top-spending customers, most popular dishes, peak ordering times, and high-performing restaurants were identified, highlighting actionable trends for business optimization.The project also emphasizes synthetic data generation using Python Faker, realistic timestamps, and Indian customer/restaurant details, making it ideal for SQL practice, analytics, and academic purposes.
       Overall, this case study provides a complete end-to-end simulation of a food delivery ecosystem, demonstrating how relational databases support data-driven decision-making and operational efficiency in real-world applications.

# Author - Vaibhav Gade
This project (zomato-db-case-study) is part of my portfolio, showcasing the SQL skills essential for data analyst roles.
