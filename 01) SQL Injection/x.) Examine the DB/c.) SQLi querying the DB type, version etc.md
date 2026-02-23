## ⛳ Lab: SQL injection attack, querying the database type and version on MySQL and Microsoft

-  This lab contains a SQL injection vulnerability in the product category filter. You can use a UNION attack
   to retrieve the results from an injected query.

- To solve the lab, display the database version string.


🍁 `Solution:`
-
1) Use Burp Suite to intercept and modify the request that sets the product category filter.

2) Determine the number of columns that are being returned by the query and which columns contain text data.
3) Verify that the query is returning two columns, both of which contain text, using a payload like the
   following in the category parameter:

       '+UNION+SELECT+'abc','def'#

4) Use the following payload to display the database version:

       '+UNION+SELECT+@@version,+NULL#


Make the database retrieve the string: '8.0.42-0ubuntu0.20.04.1'
