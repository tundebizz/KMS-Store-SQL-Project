CREATE TABLE kms_customer (
	Customer_Name VARCHAR,
	Order_ID INT PRIMARY KEY 
);

CREATE TABLE kms_order (
    Row_ID INT PRIMARY KEY,
	Order_ID INT,
	Order_Date DATE,
	Order_Priority VARCHAR,
	Order_Quantity INT,
	Sales DECIMAL (19,4),
	Discount DECIMAL (19,4),
	Ship_Mode VARCHAR,
	Profit DECIMAL (19,4),
	Unit_Price DECIMAL (19,4),
	Shipping_Cost DECIMAL (19,4),
	Customer_Name VARCHAR,
	Province VARCHAR,
	Region VARCHAR,
	Customer_Segment VARCHAR,
	Product_Category VARCHAR,
	Product_Sub_Category VARCHAR,
	Product_Container VARCHAR,
	Margin DECIMAL(19,4), 
	Ship_Date DATE,
	CONSTRAINT FK_Order_ID FOREIGN KEY (Order_ID)
    REFERENCES kms_customer(Order_ID)
);

CREATE TABLE kms_return (
	Order_ID INT,
	Status VARCHAR,
	CONSTRAINT FK_Order_ID FOREIGN KEY (Order_ID)
	REFERENCES kms_customer(Order_ID)
);

SELECT * FROM kms_order

--Case 1: Which product category had the highest sales?
SELECT product_category,SUM(Sales)
FROM kms_order
GROUP BY 1
ORDER BY 2 DESC
LIMIT 1;

--Case 2: What are the Top 3 and Bottom 3 Regions with regards to sales?
---TOP 3
SELECT region,ROUND (SUM(Sales),2) AS Sum_Of_Sales
FROM kms_order
GROUP BY 1
ORDER BY 2 DESC
LIMIT 3;

--BOTOM 3 
SELECT region,ROUND (SUM(Sales),2) AS Sum_Of_Sales
FROM kms_order
GROUP BY 1
ORDER BY 2 ASC
LIMIT 3;

--Case 3: What was the total sales of appliances in Ontario?
SELECT ROUND(SUM(Sales),2) AS Sum_Of_Sales
FROM kms_order
WHERE product_sub_category = 'Appliances' 
AND province = 'Ontario';

/*Case 4: Advise the management of KMS on what to to do to increase
the revenue from the bottom 10 customers*/
SELECT Customer_name, ROUND(SUM (sales),2) AS Sum_Of_Sales
FROM kms_order
GROUP BY 1 
ORDER by 2 ASC
LIMIT 10;

/*Case 5: KMS incurred the most shipping cost using which shipping
method?*/
SELECT ship_mode, ROUND(SUM (Shipping_Cost),2) AS Sum_Of_Shipping_Cost
FROM kms_order
GROUP BY 1
ORDER BY 2 DESC
LIMIT 1;

/*Case 6: Who are the most valuable customers */
SELECT Customer_name, ROUND(SUM (profit),2) AS Sum_Of_Profit
FROM kms_order
GROUP BY 1
ORDER BY 2 DESC
LIMIT 10;

/*Case 7: If the delivery truck is the most economical but the slowest
shipping method and Express Air is the fastest but the most expensive
one, do you think the company appropriately spent shipping costs
based on the Order Priority? Explain your answer*/
SELECT order_priority, ROUND (SUM(shipping_cost),2) AS Sum_Of_Shipping_Cost
FROM kms_order
GROUP BY 1
ORDER BY 2 DESC;

--Case 8: Which small business customer had the highest sales?
SELECT customer_name, ROUND (SUM(sales),2) AS Sum_Of_Sales
FROM kms_order
WHERE customer_segment = 'Small Business'
GROUP BY 1
ORDER BY 2 DESC
LIMIT 1;

/*Case 9: Which Corporate Customer placed the most number of orders
in 2009 – 2012? How many orders were placed by the Corporate
customer?*/
SELECT customer_name, SUM(order_quantity) AS Sum_Of_Orders
FROM kms_order
WHERE customer_segment = 'Corporate'
AND order_date 
BETWEEN '2009-01-01' AND '2012-12-31'
GROUP BY 1
ORDER BY 2 DESC
LIMIT 1;

--Case 10: Which consumer customer was the most profitable one?
SELECT customer_name, ROUND (SUM(profit),2) AS Sum_Of_Sales
FROM kms_order
WHERE customer_segment = 'Consumer'
GROUP BY 1
ORDER BY 2 DESC
LIMIT 1;

--Case 11: Which customer returned items and what segment do they belong?
--Method 1:
SELECT a.customer_name, a.order_id, c.customer_segment
FROM kms_customer a, 
	(SELECT order_id, status
	FROM kms_return
	WHERE status ='Returned')b,
	kms_order c
WHERE a.order_id = b.order_id
AND a.order_id = c.order_id
ORDER BY b.order_id

--Method 2:
SELECT a.customer_name, a.order_id
FROM kms_customer a, 
	(SELECT order_id, status
	FROM kms_return
	WHERE status ='Returned')b
WHERE a.order_id = b.order_id
ORDER BY b.order_id

SELECT DISTINCT order_id
from kms_return

SELECT order_id, status
	FROM kms_return
WHERE status ='Returned'


