## ⛳ Lab: SQLi vulnerability in WHERE clause allowing retrieval of hidden data


- This lab contains a SQLi vulnerability in the product category filter. When the user selects a category, 
  the application carries out a SQL query like the following:

      SELECT * FROM products WHERE category = 'Gifts' AND released = 1

- To solve the lab, perform a SQLi attack that causes the application to display one or more unreleased products.


[Access the Lab](https://portswigger.net/web-security/learning-paths/sql-injection/sql-injection-retrieving-hidden-data/sql-injection/lab-retrieve-hidden-data#)


### 🌴 Solution:- 
1) Change the value from `category` to `'+OR+1=1--`.
2) Submit the request and verify the response.
3) `'+OR+1=1--` query leads to the disclosure of unreleased products.
