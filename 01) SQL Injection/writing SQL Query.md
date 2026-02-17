## ⛳ Writing your 1st SQL query

- Orders (`id` , `drink`, `price`, `time`) 
- Menu (`drink`, `price`)


#### 🌴 Step 1: View Everything in a Table (Select + From)
- We start with the most basic query. When we use `SELECT*`, the `*` symbol means all columns. The word `FROM`
  tells the database which table to use.

- Try this query:

      SELECT * FROM Orders;

Run Query and every order currently stored in the database.


#### 🌴 Step 2: Show Only Specific Columns (Select Drink, Price)
- Sometimes we do not need every column. We can choose specific columns by listing them after `SELECT`.

      SELECT drink, price FROM Orders;

This will display only the drink and price columns.


#### 🌴 Step 3: Filter Results (Where)
- The `WHERE` keyword filters rows. It keeps only rows that match a condition.
- Try filtering by drink name:

      SELECT * FROM Orders WHERE drink = 'Coffee';

If the database contains coffee orders, you will now see only those rows.
- Hint: If you are not sure which drink names exist, run:

      SELECT * FROM Menu;


#### 🌴 Step 4: Sort Results (Order By)
- The `ORDER` BY keyword sorts results by a column. By default, results are sorted in ascending order 
(lowest to highest).
- Try sorting orders by price (lowest first):

      SELECT * FROM Orders ORDER BY price;

- To sort in reverse order (highest to lowest), add `DESC`.
- Try sorting orders by price (highest first):

      SELECT * FROM Orders ORDER BY price DESC;


#### 🌴 Step 5: Combine Filtering + Sorting
- Most real queries combine parts together. Here, we filter to keep only one drink type and then sort by price.
- Try this query:

      SELECT * FROM Orders WHERE drink = 'Coffee' ORDER BY price DESC;


#### 🍁 SQL Queries Learned:-

`SELECT` – choose what data to display

`FROM` – choose where the data comes from

`WHERE` – filter records based on a condition

`ORDER BY` – sort results

1) When you showed all orders, how many rows were returned?
-  50
2) When you sorted orders by price from cheapest to most expensive, which drink appeared first?
-  Tea
3) When you sorted the menu by price from most expensive to cheapest, which drink appeared first?
-  Latte


`Source`: [TryHackMe](https://tryhackme.com/room/databasesqlbasics)
