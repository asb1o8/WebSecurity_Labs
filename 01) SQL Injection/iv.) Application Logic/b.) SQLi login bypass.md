## ⛳ Lab: SQL injection vulnerability allowing login bypass


- This lab contains a SQL injection vulnerability in the login function.
- To solve the lab, perform a SQL injection attack that logs in to the application as the `administrator` user.

[Access The Lab](https://portswigger.net/web-security/learning-paths/sql-injection/sql-injection-subverting-application-logic/sql-injection/lab-login-bypass#)


### 🌴 Solution:- 
1) Access the login page by clicking on **My Account** .
2) Login as `administrator'--`
3) `administrator'--` shows *"Your username is: administrator"*, proving SQLi login bypass.
