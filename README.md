# 📝 Assignment: Database Design and Normalization

## 🎯 **Learning Objectives**
* 🛠️ **Understand the principles of good database design** and **normalization**.
* 💡 **Apply normalization techniques** to improve database structure and efficiency.
* 🔍 **Learn First, Second, and Third Normal Forms** (1NF, 2NF, 3NF) to eliminate redundancy and optimize data storage.

---

## 📋 **What You'll Need**
* 💻 A computer with internet access.
* ✍️ A code editor (e.g., Visual Studio Code).
* 🖥️ MySQL Workbench or another SQL database environment.

---


## 📝 Submission Instructions  
📂 Write all your SQL queries in the **answers.sql** file.  
✍️ Answer each question concisely and make sure your queries are clear and correct.  
🗣️ Structure your responses clearly, and use comments if necessary to explain your approach.

--- 

## 📚 Assignment Questions

---

### Question 1 Achieving 1NF (First Normal Form) 🛠️
Task:
- You are given the following table **ProductDetail**:

| OrderID | CustomerName  | Products                        |
|---------|---------------|---------------------------------|
| 101     | John Doe      | Laptop, Mouse                   |
| 102     | Jane Smith    | Tablet, Keyboard, Mouse         |
| 103     | Emily Clark   | Phone                           |


- In the table above, the **Products column** contains multiple values, which violates **1NF**.
- **Write an SQL query** to transform this table into **1NF**, ensuring that each row represents a single product for an order
- SELECT OrderID, CustomerName, ProductID, ProductName
FROM ProductDetail
CROSS APPLY (
SELECT ProductName, ProductID
FROM Products
) AS p
ORDER BY OrderID, ProductName;
SQL query is used to transform the ‘ProductDetail’ table into 1NF, ensuring that each row represents a single product for an order.
The query uses the ‘CROSS APPLY’ clause to apply a subquery to each row in the ‘ProductDetail’ table. The subquery is used to split the ‘Products’ column into separate rows, each containing a single product. The ‘SELECT’ statement in the subquery is used to specify the columns that need to be retrieved from the ‘Products’ table, in this case, the ProductName and ProductID columns.
The ‘AS’ clause is used to give an alias to the subquery result, in this case, ‘p’. This makes the query easier to read and write.
The ‘ORDER BY’ clause is used to sort the results by the OrderID and ProductName columns.
The final result is a table with three columns: OrderID, CustomerName, and ProductName. Each row in the table represents a single product for an order.

--- 

### Question 2 Achieving 2NF (Second Normal Form) 🧩

- You are given the following table **OrderDetails**, which is already in **1NF** but still contains partial dependencies:

| OrderID | CustomerName  | Product      | Quantity |
|---------|---------------|--------------|----------|
| 101     | John Doe      | Laptop       | 2        |
| 101     | John Doe      | Mouse        | 1        |
| 102     | Jane Smith    | Tablet       | 3        |
| 102     | Jane Smith    | Keyboard     | 1        |
| 102     | Jane Smith    | Mouse        | 2        |
| 103     | Emily Clark   | Phone        | 1        |

- In the table above, the **CustomerName** column depends on **OrderID** (a partial dependency), which violates **2NF**. 

- Write an SQL query to transform this table into **2NF** by removing partial dependencies. Ensure that each non-key column fully depends on the entire primary key.

- SELECT OrderID, CustomerName, ProductID, ProductName, Quantity
FROM OrderDetails
CROSS APPLY (
SELECT ProductName, ProductID
FROM Products
) AS p
ORDER BY OrderID, ProductName;
SQL query is used to transform the ‘OrderDetails’ table into 2NF, ensuring that each non-key column fully depends on the entire primary key.
The query uses the ‘CROSS APPLY’ clause to apply a subquery to each row in the ‘OrderDetails’ table. The subquery is used to split the ‘Products’ column into separate rows, each containing a single product. The ‘SELECT’ statement in the subquery is used to specify the columns that need to be retrieved from the ‘Products’ table, in this case, the ProductName and ProductID columns.
The ‘AS’ clause is used to give an alias to the subquery result, in this case, ‘p’. This makes the query easier to read and write.
The ‘ORDER BY’ clause is used to sort the results by the OrderID and ProductName columns.
The final result is a table with four columns: OrderID, CustomerName, ProductID, and ProductName. Each row in the table represents a single product for an order, and the Quantity column is also included. The table is now in 2NF, as each non-key column fully depends on the entire primary key.

---
Good luck 🚀
