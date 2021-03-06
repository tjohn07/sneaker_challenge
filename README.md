Summer 2022 Data Science Intern Challenge

Please see my responses in the ReadMe below. You can also see my code for the first challenge in the 'sneakers' notebook, and all answers are also in the .txt file.


### Question 1: Given some sample data, write a program to answer the following: click here to access the required data set

On Shopify, we have exactly 100 sneaker shops, and each of these shops sells only one model of shoe. We want to do some analysis of the average order value (AOV). When we look at orders data over a 30 day window, we naively calculate an AOV of $3145.13. Given that we know these shops are selling sneakers, a relatively affordable item, something seems wrong with our analysis.

Think about what could be going wrong with our calculation. Think about a better way to evaluate this data.

* The issue that we're running into is that we're calculating the average, but some orders are for a significant amount of pairs of shoes, indicating that these orders may be for resale. In order to determine the true average order amount, we should consider taking a look at the average of all orders falling below the 75th percentile. We can also consider the median order amount, which may give us a more balanced idea of order amounts.

What metric would you report for this dataset?

* I would report mean for order amounts falling below the 75th percentile and I would report the median for the full dataset.


What is its value?

* Calculating the median, the average order amount is $284.00.
* Calculating the mean for the data following below the 75th percentile, we can consider our actual average order to be approximately $233.00.


### Question 2: For this question you’ll need to use SQL. Follow this link to access the data set required for the challenge. Please use queries to answer the following questions. Paste your queries along with your final numerical answers below.

How many orders were shipped by Speedy Express in total?

SELECT COUNT(*) FROM [Orders] WHERE ShipperID = 1;

* Answer: 54

What is the last name of the employee with the most orders?

SELECT MAX (mycount), EmployeeID
FROM (SELECT EmployeeID,COUNT(EmployeeID) mycount
FROM Orders
GROUP BY EmployeeID);

SELECT LastName FROM [Employees] WHERE EmployeeID = 4;

* Answer: Peacock

What product was ordered the most by customers in Germany?

CREATE VIEW german_cust AS
SELECT c.CustomerID
FROM Customers as c
WHERE c.Country = 'Germany';

CREATE VIEW german_orders AS
SELECT *
FROM german_cust
INNER JOIN Orders as o
ON german_cust.CustomerID = o.CustomerID;

CREATE VIEW german_products AS
SELECT *
FROM german_orders
INNER JOIN OrderDetails as o
ON german_orders.OrderID = o.OrderID;

SELECT MAX (mycount), ProductID
FROM (SELECT ProductID,COUNT(ProductID) mycount
FROM german_products
GROUP BY ProductID);

* ProductID = 31

SELECT ProductName FROM Products WHERE ProductID = 31;

* Answer: Gorgonzola Telino
