# Shopify Data Science Internship Application

### Question 1

First, load the data and plot it.


```python
import pandas as pd
orders = pd.read_csv('2019 Winter Data Science Intern Challenge Data Set - Sheet1.csv')
orders["order_amount"].hist()
```




    <matplotlib.axes._subplots.AxesSubplot at 0x114f37f28>




    
![png](Question%201_2_1.png)
    


After plotting the distribution of order_amount, I can see that there are a few orders that are much larger than the regular orders. These outliers made it so that the average is much larger than expected. Instead of using the average order value, it would be better to use the median order value so that these outliers don't skew our metric.


```python
print("The median order value is: ", orders["order_amount"].median())
```

    The median order value is:  284.0


### Question 2
**a. How many orders were shipped by Speedy Express in total?**
```sql
SELECT COUNT(ShipperName) 
FROM Shippers JOIN Orders ON Shippers.ShipperID = Orders.ShipperID
WHERE ShipperName = "Speedy Express";
```

Answer: 54

**b. What is the last name of the employee with the most orders?**
```sql
SELECT LastName
FROM Orders JOIN Employees ON Orders.EmployeeID = Employees.EmployeeID
GROUP BY Orders.EmployeeID 
ORDER BY COUNT(OrderID) DESC
LIMIT 1;
```

Answer: Peacock

**c. What product was ordered the most by customers in Germany?**

There are two different ways to interpret this question. 

Interpretation 1: The product that was ordered the most times by customers in Germany (ignoring quantity in each order) was Gorgonzola Telino. I used the following query:

```sql
SELECT ProductName
FROM Orders 
JOIN Customers ON Orders.CustomerID = Customers.CustomerID
JOIN OrderDetails ON Orders.OrderID = OrderDetails.OrderID
JOIN Products ON Products.ProductID = OrderDetails.ProductID
WHERE Country = "Germany"
GROUP BY Products.ProductID
ORDER BY COUNT(Products.ProductID) DESC
LIMIT 1
```

Interpretation 2: The product with the highest total quantity ordered by customers in Germany was Boston Crab Meat. I used the following query:

```sql
SELECT sum(Quantity)
FROM Orders 
JOIN Customers ON Orders.CustomerID = Customers.CustomerID
JOIN OrderDetails ON Orders.OrderID = OrderDetails.OrderID
JOIN Products ON Products.ProductID = OrderDetails.ProductID
WHERE Country = "Germany"
GROUP BY ProductName
ORDER BY sum(Quantity) DESC
LIMIT 1
```
