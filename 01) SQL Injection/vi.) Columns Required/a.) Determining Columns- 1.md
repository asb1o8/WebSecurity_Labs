## ⛳ Determining the number of columns required

- When we perform a SQLi UNION attack, there are two effective methods to determine how many columns are being 
  returned from the original query.
- One method involves injecting a series of `UNION BY` clauses and incrementing the specified column index until 
  an error occurs. For example, if the injection point is a quoted string within the `WHERE` clause of the
  original query, you would submit:
  
      ' ORDER BY 1--
      ' ORDER BY 2--
      ' ORDER BY 3--
        etc.

- This series of payloads modifies the original query to order the results by different columns in the result
  set. The column in an `ORDER BY` clause can be specified by its index, so you don't need to know the names of
  any columns. When the specified column index exceeds the number of actual columns in the result set, the
  database returns an error, such as:
  
      The ORDER BY position number 3 is out of range of the number of items in the select list.

- The application might actually return the database error in its HTTP response, but it may also issue a generic
  error response. In other cases, it may simply return no results at all. Either way, as long as you can detect
  some difference in the response, you can infer how many columns are being returned from the query.



🎋 `Terms Explained` :-
-
1) `If the injection point is a quoted string`
   - Quoted Strings are values wrapped in `'single quotes'` or `"double quotes"`

         SELECT * FROM users WHERE username = 'Alice' OR '1'='1';

2) `This series of payloads modifies the original query to order the results by different columns in the result set.` 

  - Normally, a SQL query might look like:

        SELECT * FROM users WHERE username = 'Alice';
    
- Attackers can inject extra SQL code into the query. In this case, the payloads are designed to modify the
  query’s ORDER BY clause.

3) `Issuing a Generic Response Error` means:-
  - It is a vague, user-friendly message that doesn’t reveal sensitive technical details.
  - Returning the actual database error: e.g., “SQL syntax error near ‘FROM’”. This reveals technical about what                                          went wrong.
  - Issue a generic error response: e.g., “Something went wrong. Please try again later.”


4) `Inferring the Columns being Returned from a Query` means:-
  - In the context of SQLi or query testing, attackers often try to figure out how many columns a query is returning.
  - They do this by *sending crafted inputs and observing differences in the application’s responses*
  - If the *query expects 3 columns but you force it to return 4, the application might throw an error or behave     differently*.
  - By gradually adjusting and watching the response, you can infer(no. of columns the DB would present) the number of columns in the query.
  - This matters because knowing the column count helps attackers align their injected data with the query structure, making exploitation possible.

5) `Common DB Errors that leak info` are as:-

  - Syntax Errors:
      - Example: “You have an error in your SQL syntax near ‘FROM users’”.
      - Clue: Reveals the type of database (MySQL, PostgreSQL, Oracle, etc.) and sometimes the exact query fragment.

  - Column/Field Errors:
       - Example: “Unknown column ‘email_address’ in ‘field list’”.
       - Clue: Exposes actual column names in the database schema.

  - Table Errors:
       - Example: “Table ‘customers’ doesn’t exist”.
       - Clue: Reveals table names and structure.

  - Type Mismatch Errors:
       - Example: “Conversion failed when converting varchar to int”.
       - Clue: Indicates the data type of a column, helping attackers craft more precise injections.

  - Constraint/Key Errors:
       - Example: “Duplicate entry ‘123’ for key ‘PRIMARY’”.
       - Clue: Shows which columns are unique or primary keys.

  - Driver/Connection Errors:
       - Example: “ODBC driver error” or “ORA-00933: SQL command not properly ended”.
       - Clue: Reveals the database engine or driver in use.
