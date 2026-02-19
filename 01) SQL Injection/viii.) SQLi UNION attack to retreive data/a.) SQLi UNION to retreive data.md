## ⛳ Using a SQLi UNION attack to retrieve interesting data

- When you have determined the number of columns returned by the original query and found which columns can hold 
  string data, you are in a position to retrieve interesting data. Suppose that:

    - The original query returns two columns, both of which can hold string data.
    - The injection point is a quoted string within the `WHERE` clause.
    - The database contains a table called `users` with the columns `username` and `password`.

- In this example, we can retrieve the contents of the users table by submitting the input:

      ' UNION SELECT username, password FROM users--

- In order to perform this attack, you need to know that there is a table called `users` with two columns called
  `username` and `password`. Without this information, you would have to guess the names of the tables and
  columns. All modern databases provide ways to examine the database structure, and determine what tables and
  columns they contain.

🎋 `Deeply Explored`
-

  - When application draft a SQL query, that includes the user input.
  - If developer concatenate the input directly with the query then database will treat that as part of query,
    rather than normal string.
  - Casue of this attacker got succeed into injecting the code.

        user_input = "abc' OR '1'='1"
        query = "SELECT * FROM users WHERE name = '" + user_input + "';"

- 👉 Database will execute it as valid query:

      SELECT * FROM users WHERE name = 'abc' OR '1'='1';

💡 For Easier note:
If you build queries by concatenating user input, they can be broken. If you use parameterization, the query 
stays safe.
