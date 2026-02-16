## ⛳ SQLi *UNION* attack

- `UNION` is a SQL keyword that lets you combine results from two different queries into one output. In a SQLi attack,
  the attacker adds UNION to the vulnerable query so they can attach another query that pulls data from a different
  table.
  
- Let's suppose the app runs this query:

      SELECT name, email FROM users WHERE id = '1';

     If it’s vulnerable, an attacker could inject:

      ' UNION SELECT username, password FROM accounts --
    
Now the database combines the original results (name, email from users) + the attacker’s results 
(username, password from accounts)

###

-  The `UNION` keyword enables you to execute one or more additional `UNION`SELECT queries and append the
   results to the original query. For example:

        SELECT a, b FROM table1 UNION SELECT c, d FROM table2

- This SQL query returns a single result set with two columns, containing values from columns `a` and `b`
  in `table1`  and columns `c` and `d` in `table2`. 


🎋 `UNION attack explored`:-
-
 - Combines results of multiple queries, `UNION` attacks are used to leak sensitive data by aligning column counts and types, not just to merge identical answers.
 - It’s not about combining *“same answers”* (like Mumbai appearing in two different columns), but about **forcing the application to reveal data from other tables** or columns that the attacker shouldn’t normally see.
