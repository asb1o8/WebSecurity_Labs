## ⛳ Lab: SQL injection vulnerability in WHERE clause allowing retrieval of hidden data


- This lab contains a SQL injection vulnerability in the product category filter. When the user selects a category, the application carries out a SQL query like 
the following:

      SELECT * FROM products WHERE category = 'Gifts' AND released = 1

- To solve the lab, perform a SQL injection attack that causes the application to display one or more unreleased products.
[ACCESS THE LAB](https://portswigger.net/academy/labs/launch/d9a071d8264e85184722707ff5747bbbd77963967d1d01f1b22f5dd8252f9767?referrer=%2fweb-security%2fsql-injection%2flab-retrieve-hidden-data)


#### 🌴 Steps to inject the SQL:-
1) Access the gift category.
2) Modify the `category` parameter, with the value `'+OR+1=1--`
3) Above injection revealed all the unreleased or hidden products.
