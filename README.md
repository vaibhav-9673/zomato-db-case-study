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




## 📊 Example Queries
## 1. Customer Analytics
#### A) Who are the top 10 customers by total spending?
#### B) Which customers placed more than 1 orders?
#### C) Which customers have ordered from multiple restaurants?
#### D) Which customer ordered the highest number of items overall?
#### E) What is the average order value per customer?

## 2. Restaurant Performance
#### A) Which restaurant earned the most revenue?
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



