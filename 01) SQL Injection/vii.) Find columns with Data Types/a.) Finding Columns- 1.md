## ⛳ Finding columns with a useful data type

- A SQL injection `UNION` attack enables you to retrieve the results from an injected query. The interesting data
  that you want to retrieve is normally in string form. This means you need to find one or more columns in the
  original query results whose data type is, or is compatible with, string data.

-  After you determine the number of required columns, you can probe each column to test whether it can hold
   string data. You can submit a series of `UNION SELECT` payloads that place a string value into each column in
   turn. For example, if the query returns four columns, you would submit:
   
       ' UNION SELECT 'a',NULL,NULL,NULL--
       ' UNION SELECT NULL,'a',NULL,NULL--
       ' UNION SELECT NULL,NULL,'a',NULL--
       ' UNION SELECT NULL,NULL,NULL,'a'--

-  If the column data type is not compatible with string data, the injected query will cause a database error,
     such as:

       Conversion failed when converting the varchar value 'a' to data type int.

- If an error does not occur, and the application's response contains some additional content including the
  injected string value, then the relevant column is suitable for retrieving string data.



### 🎋 `Deeply Explored`

#### 🔺 CONCEPT 1:-
 `A SQL injection UNION.....with string data`

a) If original query are of 3 columns then, injected query must be of 3 columns. Example:
   
       SELECT id, name, age FROM users
       UNION
       SELECT 1, 'Injected', 25;

b) Data type must match:
- If original query's column type is `VARCHAR` then, in the injected query you also have to provide a string 
for that column.
- Error will occur if any mismatch.

c) String Column is necessary:
- Sensitive data(username, password, email) mostly are in string form.
- Therefore, Attacker needs the same kind of column which accepts the string data type.

      UNION SELECT 'admin:password', NULL, NULL;
  
🎯 Flow of Attack
- Step 1: An attacker checks how many columns the query returns. (`ORDER BY` ya `UNION SELECT NULL`,... se).
- Step 2: Identify which column accepts string data.
- Step 3: Injects the sensitive data in that column (like- username || ':' || password).
- Step 4: The attacker obtains the original data along with the injected sensitive data in the output.



- A SQLi `UNION` attack means merging the original query result with the attacker’s own query. This is only 
possible when the number of columns and their data types match. Because sensitive data is usually stored as 
strings, the attacker needs a column that accepts string data. If such a column exists, the attacker can 
showcase their injected data in the output.

👉 In short: UNION attack = own result + original result. 
  - String column = key to extract useful data.


#### 🔺 CONCEPT 2:-
 `After you determine.....NULL,'a'--`

##### 🔎 Context:
When attacker use the `UNION SELECT`, he have to ensure that the column's count & data type match. Attacker also 
have to check which column accept the string data type, as sensitive info (username, password, email) is in 
string format.

🔎 Finding Column count:
- Attacker checks the no. of columns, query is returning.
- example: If query returns 4 columns, then attacker injects 4 columns in query.

🧪 String compatibility test:
- Now, attacker injects string in each column and test which column accepts the string. Will attempts
  multiple payloads:

      ' UNION SELECT 'a',NULL,NULL,NULL--
      ' UNION SELECT NULL,'a',NULL,NULL--
      ' UNION SELECT NULL,NULL,'a',NULL--
      ' UNION SELECT NULL,NULL,NULL,'a'--

- In each payload there's 'a' (string), rest are NULL.

🧚‍♂️ Result observation:
- If query succeeds then output showed as 'a', means that column accepts the string data.
- If Error, column is not comptaible for string (maybe INT or DATA type).

- In `UNION` injection, attacker first finds the number of counts in the column then test each column which 
  accepts the string data type.
- Attacker test this putting 'a' in each column, rest columns as NULL.
- Whichever the column are comptaible for string, using that column attacker can show the sensitive data as
  output.


  #### 🔺 CONCEPT 3:-
  
 `If the column data type.....retrieving string data.`
  - If Error → column string not accepted.
  - If no Error + string showed in output → column string accepted.

💡 Memory Trick:
“Error = mismatch, Output = match.”
