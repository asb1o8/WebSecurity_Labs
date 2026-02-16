##  ⛳ Determining the number of columns required- 2

- The second method involves submitting a series of `UNION SELECT` payloads specifying a different number of null 
  values:
  
      ' UNION SELECT NULL--
      ' UNION SELECT NULL,NULL--
      ' UNION SELECT NULL,NULL,NULL--
        etc.
  
  - If the number of nulls does not match the number of columns, the database returns an error, such as:

        All queries combined using a UNION, INTERSECT or EXCEPT operator must have an equal number of expressions in their target lists.

- We use `NULL` as the values returned from the injected `SELECT` query because the data types in each column      must be compatible between the original and the injected queries. `NULL` is convertible to every common data     type, so it maximizes the chance that the payload will succeed when the column count is correct.
- As with the `ORDER BY` technique, the application might actually return the database error in its HTTP response,   but may return a generic error or simply return no results. When the number of nulls matches the number of columns, the database returns an additional row in the result set, containing null values in each column.
- The effect on the HTTP response depends on the application's code(coding style of app). If you are lucky, you will see some extra response, such as an extra row on an HTML table. Otherwise, the null values might show a different error, such as a `NullPointerException`. In the worst case, If the application hides the error and shows a normal‑looking page, the attacker cannot tell whether their test worked or failed, so the technique doesn’t help them.


🎋 `Deeply Explored`:-
-

   -  `' UNION SELECT NULL--`
         - Attacker injected the payload: A NULL is given means a Column is being tested here.

   -  `' UNION SELECT NULL,NULL--`
         - 2 NULL is given here → means Attacker is checking whether the query are of 2 columns or not.

   -  `' UNION SELECT NULL,NULL,NULL--`
         - Now 3 columns are being tested.
    
 #### ⚙️ Why do we ue NULL?
  - NULL is a universal placeholder.
  - NULL is acceptable in all data type columns(string, number, date, etc.).
  - Therefore when the Attacker inject NULL, that is safe and query will not give error, doesn't matter the type of Column.

        ' UNION SELECT NULL,NULL,NULL--

Result would be:- `id` (integer), `Name` (text), `dob` (date)
