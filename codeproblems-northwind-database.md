Do all the NorthWind database work in brand new MySQL container named `mysql_northwind`

`docker run --name mysql_northwind -e MYSQL_ROOT_PASSWORD=password123  -p 3307:3306 -e MYSQL_EXTRA_FLAGS="--max_connections=50"  bitnami/mysql:latest`



run the northwind database scripts on the mysql client

first login

`mysql -u root -p -h 127.0.0.1 -P 3307`

then 

`source ~/Downlaods/northwind.sql`

`source ~/Downlaods/northwind-data.sql`





Here are SQL questions for the Microsoft Northwind database, categorized into Easy, Medium, and Difficult levels to help practice SQL skills:

### **Easy Level**
1. **List of Products**
   - Write a query to retrieve the `ProductName` and `UnitPrice` of all products from the `Products` table.

2. **Customers in Specific Countries**
   - Retrieve the names of all customers (`CustomerID`, `CompanyName`) located in the USA from the `Customers` table.

3. **Order Details for a Specific Order**
   - Write a query to fetch the `ProductID`, `Quantity`, and `UnitPrice` for a specific order (OrderID: 10248) from the `Order Details` table.

4. **Count of Employees**
   - Write a query to count the total number of employees in the `Employees` table.

5. **List of Categories**
   - Display all the categories (`CategoryID`, `CategoryName`) from the `Categories` table.

6. **Products with Stock Less Than 10**
   - List all products (`ProductName`) that have a stock quantity (`UnitsInStock`) of less than 10 in the `Products` table.

### **Medium Level**
1. **Orders Placed by a Specific Customer**
   - Write a query to fetch the `OrderID`, `OrderDate`, and `ShipCountry` for orders placed by the customer with `CustomerID` "ALFKI".

2. **Product Sales Summary**
   - Write a query to calculate the total sales for each product. Use `ProductID`, `Quantity`, and `UnitPrice` from the `Order Details` table to compute the total sales amount.

3. **Employee Sales by Country**
   - Write a query to display each employee's full name (`FirstName`, `LastName`) and the total number of orders they handled, grouped by their `Country` of residence in the `Employees` table.

4. **List of Products by Supplier**
   - Write a query to list the `SupplierID`, `CompanyName` (from `Suppliers`), and all `ProductNames` they supply, using a JOIN between the `Products` and `Suppliers` tables.

5. **Top 5 Most Expensive Products**
   - Write a query to list the top 5 products with the highest unit price (`UnitPrice`) in descending order from the `Products` table.

6. **Orders Shipped After the Order Date**
   - Write a query to find all orders where the `ShippedDate` is greater than the `OrderDate` in the `Orders` table.

### **Difficult Level**
1. **Customers with No Orders**
   - Write a query to find all customers (`CustomerID`, `CompanyName`) who have not placed any orders. (Hint: Use a LEFT JOIN between `Customers` and `Orders` and filter out NULLs.)

2. **Total Sales by Country**
   - Write a query to compute the total sales amount (sum of `Quantity * UnitPrice` from `Order Details`) for each country, using data from `Orders`, `Order Details`, and `Customers` tables.

3. **Employee Order Summary**
   - Write a query to generate a summary report for each employee showing their `EmployeeID`, full name (`FirstName`, `LastName`), total number of orders they handled, and the sum of sales (`Quantity * UnitPrice`). Use a JOIN between `Employees`, `Orders`, and `Order Details`.

4. **Products with Higher than Average Price in Their Category**
   - Write a query to list all products (`ProductID`, `ProductName`) that have a price (`UnitPrice`) higher than the average price of products within their respective category. (Hint: Use a subquery to calculate the average price by category.)

5. **Monthly Sales Report**
   - Write a query to display the total sales amount (sum of `Quantity * UnitPrice`) grouped by month and year of the `OrderDate` in the `Orders` table. (Hint: Use date functions to extract month and year.)

6. **Identify Customers with Repeat Orders**
   - Write a query to identify customers (`CustomerID`, `CompanyName`) who have placed more than one order. (Hint: Use the `GROUP BY` clause with a `HAVING` condition.)

These questions provide a range of difficulty and cover various SQL concepts, including basic retrieval, aggregation, filtering, and joining across multiple tables.