# 🛒 Zepto E-commerce SQL Data Analysis

A real-world **SQL Data Analyst portfolio project** based on an e-commerce inventory dataset inspired by Zepto, one of India's leading quick-commerce platforms.

This project demonstrates an end-to-end data analysis workflow using **PostgreSQL**, covering data exploration, data cleaning, and business-focused SQL analysis.

---

## 📌 Project Overview

The objective of this project is to analyze e-commerce inventory data and extract meaningful business insights using SQL.

The project covers:

* 🗄️ Database and table creation
* 🔍 Exploratory Data Analysis (EDA)
* 🧹 Data cleaning and preprocessing
* 💰 Pricing and discount analysis
* 📦 Inventory and stock analysis
* 📊 Category-level analysis
* 💡 Business-oriented SQL queries
* 📈 Revenue and product performance analysis

This project is designed to demonstrate practical SQL skills that are commonly used in **Data Analyst, Business Analyst, Retail Analytics, and E-commerce Analytics** roles.

---

## 🛠️ Tech Stack

| Technology     | Purpose                                     |
| -------------- | ------------------------------------------- |
| **PostgreSQL** | Database management and SQL analysis        |
| **pgAdmin**    | Database administration and query execution |
| **SQL**        | Data exploration, cleaning, and analysis    |
| **CSV**        | Dataset storage and import                  |

---

## 📁 Dataset

The dataset contains e-commerce product and inventory information.

Each row represents a unique **SKU (Stock Keeping Unit)**.

Duplicate product names may exist because the same product can be available in different package sizes, weights, discounts, or categories.

### Dataset Source

The dataset was sourced from Kaggle and was originally scraped from Zepto's product listings.

**Dataset:** Zepto Inventory Dataset

---

## 📊 Dataset Columns

| Column                   | Description                                   |
| ------------------------ | --------------------------------------------- |
| `sku_id`                 | Unique identifier for each product entry      |
| `name`                   | Product name                                  |
| `category`               | Product category                              |
| `mrp`                    | Maximum Retail Price                          |
| `discountPercent`        | Discount percentage applied to MRP            |
| `discountedSellingPrice` | Final selling price after discount            |
| `availableQuantity`      | Available inventory quantity                  |
| `weightInGms`            | Product weight in grams                       |
| `outOfStock`             | Indicates whether the product is out of stock |
| `quantity`               | Number of units per package                   |

> **Note:** The original price values were stored in paise and converted into Indian Rupees during data cleaning.

---

# 🔧 Project Workflow

## 1. 🗄️ Database & Table Creation

A PostgreSQL table was created with appropriate data types for each column.

```sql
CREATE TABLE zepto (
    sku_id SERIAL PRIMARY KEY,
    category VARCHAR(120),
    name VARCHAR(150) NOT NULL,
    mrp NUMERIC(8,2),
    discountPercent NUMERIC(5,2),
    availableQuantity INTEGER,
    discountedSellingPrice NUMERIC(8,2),
    weightInGms INTEGER,
    outOfStock BOOLEAN,
    quantity INTEGER
);
```

---

## 2. 📥 Data Import

The dataset was imported into PostgreSQL using **pgAdmin**.

Alternatively, PostgreSQL's `COPY` command can be used:

```sql
\copy zepto(
    category,
    name,
    mrp,
    discountPercent,
    availableQuantity,
    discountedSellingPrice,
    weightInGms,
    outOfStock,
    quantity
)
FROM 'data/zepto_v2.csv'
WITH (
    FORMAT csv,
    HEADER true,
    DELIMITER ',',
    QUOTE '"',
    ENCODING 'UTF8'
);
```

### Encoding Issue

During the import process, an encoding issue was encountered with the CSV file.

The issue was resolved by saving the dataset using **CSV UTF-8 format** before importing it into PostgreSQL.

---

# 🔍 Exploratory Data Analysis

The initial analysis focused on understanding the structure and quality of the dataset.

### Analysis performed:

* Total number of products
* Sample records from the dataset
* Null value analysis
* Number of unique product categories
* In-stock vs out-of-stock products
* Duplicate product names
* Product and SKU distribution
* Pricing distribution
* Discount distribution

---

# 🧹 Data Cleaning

Several data quality issues were identified and handled before performing business analysis.

### Cleaning operations included:

* Identifying null values
* Identifying invalid pricing records
* Removing products with zero MRP
* Removing products with zero selling price
* Converting prices from **paise to Indian Rupees**
* Validating product weights and quantities
* Checking stock availability values

Example:

```sql
UPDATE zepto
SET mrp = mrp / 100,
    discountedSellingPrice = discountedSellingPrice / 100;
```

---

# 📊 Business Analysis

After cleaning the dataset, SQL queries were used to answer practical business questions.

### 💰 Pricing & Discount Analysis

* Identify the top 10 products with the highest discounts
* Find products with high MRP and minimal discounts
* Analyze average discounts across categories
* Compare MRP with discounted selling prices
* Identify the most heavily discounted products

### 📦 Inventory Analysis

* Identify products currently out of stock
* Find high-value products that are out of stock
* Analyze inventory availability across categories
* Calculate total inventory quantity
* Measure total inventory weight by category

### 📈 Revenue Analysis

* Estimate potential revenue by product
* Calculate estimated revenue by category
* Identify categories with the highest potential revenue
* Analyze the relationship between pricing, discounts, and inventory

### ⚖️ Product Value Analysis

* Calculate price per gram
* Identify value-for-money products
* Categorize products based on weight
* Compare product prices across different package sizes

---

# 🧠 Key SQL Concepts Used

This project demonstrates practical use of:

* `SELECT`
* `WHERE`
* `GROUP BY`
* `ORDER BY`
* `HAVING`
* `DISTINCT`
* `COUNT()`
* `SUM()`
* `AVG()`
* `MIN()`
* `MAX()`
* `CASE`
* `COALESCE`
* `NULL` handling
* Aggregate functions
* Subqueries
* Common Table Expressions (CTEs)
* Window Functions
* Ranking
* Data cleaning with `UPDATE`
* Filtering and conditional analysis

---

# 📂 Project Structure

```text
zepto-sql-project/
│
├── data/
│   └── zepto_v2.csv
│
├── zepto_SQL_data_analysis.sql
│
└── README.md
```

---

# 🚀 How to Run the Project

### 1. Clone the repository

```bash
git clone https://github.com/srijan140988/zepto-sql-project.git
```

### 2. Navigate into the project

```bash
cd zepto-sql-project
```

### 3. Create a PostgreSQL database

Create a new database using PostgreSQL or pgAdmin.

### 4. Run the SQL file

Open:

```text
zepto_SQL_data_analysis.sql
```

Run the SQL queries in PostgreSQL/pgAdmin.

### 5. Import the dataset

Import:

```text
data/zepto_v2.csv
```

into the `zepto` table.

### 6. Run the analysis

Execute the SQL queries provided in the project file to reproduce the analysis.

---

# 💡 Business Questions Answered

This project uses SQL to answer questions such as:

1. Which products offer the highest discounts?
2. Which products have the highest MRP?
3. Which high-value products are currently out of stock?
4. Which categories offer the highest average discounts?
5. What is the estimated revenue potential of each category?
6. Which products provide the best price per gram?
7. How much inventory is available across different categories?
8. Which product categories contain the most inventory?
9. How does product weight affect pricing?
10. Which products have high prices but relatively low discounts?

---

# 🎯 Skills Demonstrated

Through this project, I practiced and demonstrated:

**SQL & Database**

* PostgreSQL
* Database design
* Data import
* Data cleaning
* SQL querying

**Data Analysis**

* Exploratory Data Analysis
* Data validation
* Aggregation
* Trend and category analysis
* Business problem solving

**Business Analytics**

* Pricing analysis
* Discount analysis
* Inventory analysis
* Revenue estimation
* Product comparison

---

# 📌 Project Purpose

This project was built as part of my **Data Analytics learning and portfolio development** to strengthen my practical SQL skills and demonstrate how SQL can be used to solve real-world business problems.

---

## 👨‍💻 About Me

**Srijan Verma**

Computer Science student passionate about **Data Analytics, SQL, Software Development, AI/ML, and building real-world technology solutions.**

I am currently strengthening my skills in:

* SQL
* Python
* Data Analytics
* PostgreSQL
* Data Visualization
* Machine Learning
* Generative AI

### 🔗 Connect With Me

* **GitHub:** [srijan140988](https://github.com/srijan140988)

---

## ⭐ If You Found This Project Useful

If this project helped you learn SQL or data analytics, feel free to **⭐ star the repository**.

Feedback and suggestions are always welcome!

---

**Built with SQL & PostgreSQL | Data Analytics Portfolio Project 🚀**
