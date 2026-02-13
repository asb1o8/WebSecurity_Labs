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



##### 🎋 Terms Explained:-
1) `If the injection point is a quoted string`
   - Quoted Strings are values wrapped in `'single quotes'` or `"double quotes"`

         SELECT * FROM users WHERE username = 'Alice' OR '1'='1';

2.) `This series of payloads modifies the original query to order the results by different columns in the result set.` 

  - Normally, a SQL query might look like:

        SELECT * FROM users WHERE username = 'Alice';
    
- Attackers can inject extra SQL code into the query. In this case, the payloads are designed to modify the
  query’s ORDER BY clause.
