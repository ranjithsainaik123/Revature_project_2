Star Schema: 

1. A star schema is a type of database schema commonly used in data warehouse environments like BigQuery.
2. In a star schema, data is organized into two types of tables: fact tables and dimension tables.

 Fact Tables: 

1. The fact table contains quantitative and numeric performance measures or metrics, often referred to as facts.
2. Each row in the fact table represents a specific event or transaction and contains foreign key references to related dimensions.

 Dimension Tables: 

Dimension tables contain descriptive information or attributes that provide context to the data in the fact table.

 In a star schema: 

1. The fact table is at the center, representing the core business data.
2. Dimension tables surround the fact table, connecting to it through foreign key relationships.
3. The star schema simplifies queries and enables efficient reporting because it reduces the number of joins needed to retrieve relevant data.

my_sql Code:

CREATE DATABASE PROJECT2;
USE PROJECT2;

-----------------------------------------------------------------------
-----------------------------------------------------------------------
drop table if exists customer_location;

CREATE TABLE customer_location (
    LocationID INT PRIMARY KEY,
    county VARCHAR(255),
    region VARCHAR(255),
    city VARCHAR(255),
    state varchar(225),
    zip VARCHAR(20)
);

-------------------------------------------------------------------------
-------------------------------------------------------------------------
drop table if exists products;
CREATE TABLE Products (
    ProductID INT PRIMARY KEY,
    category VARCHAR(255),
    sku VARCHAR(255),
    Price FLOAT(2)
);

--------------------------------------------------------------------------
--------------------------------------------------------------------------
drop table if exists customers;
CREATE TABLE Customers (
    CustID INT PRIMARY KEY,
    Age INTEGER,
    First_Name VARCHAR(255),
    Last_Name VARCHAR(255),
    Gender VARCHAR(10),
    Email VARCHAR(255),
    Customer_Since DATETIME,
    SSN VARCHAR(20),
    Phone_Number VARCHAR(20),
    User_Name VARCHAR(50),
    Prefix VARCHAR(20)
);

--------------------------------------------------------------------------
--------------------------------------------------------------------------
drop table if exists transaction_line;
CREATE TABLE transaction_line (
    Order_ID INT PRIMARY KEY,
    Item_ID INT,
    Qty_Ordered INT,
    Price_per_unit FLOAT(2),
    Subtotal FLOAT(2),
    Discount_Amount FLOAT(2),
    discount_percent float(2),
    Total FLOAT(2),
    status varchar(225),
    payment_method varchar(225)
);

---------------------------------------------------------------------------
---------------------------------------------------------------------------

DROP TABLE IF EXISTS ORDERS;
CREATE TABLE Orders (
    Order_ID INT,
    CustID INT,
    ProductID INT,
    LocationID INT,
    Order_Date DATETIME,
    DiscountPercent FLOAT(2),
    Subtotal FLOAT(2),
    Billing_Status VARCHAR(255),
    Month INT,
    Year INT,
    QtyOrdered INT,
    FOREIGN KEY (ORDER_ID) REFERENCES TRANSACTION_LINE(ORDER_ID),
    FOREIGN KEY (CustID) REFERENCES Customers(CustID),
    FOREIGN KEY (ProductID) REFERENCES Products(ProductID),
    FOREIGN KEY (LocationID) REFERENCES customer_location(LocationID)
);
