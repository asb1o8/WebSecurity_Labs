
#### 🌴 SQL Injection:-
SQL injection (SQLi) is a web security vulnerability that allows an attacker to interfere with the queries that an application makes to its database. 
This can allow an attacker to view data that they are not normally able to retrieve.


#### 🌴 Impact of a successful SQL injection ?

A successful injection can result in unauthorized access to sensitive data, such as:

    - Passwords.
    - Credit card details.
    - Personal user information.

These have caused reputational damage and regulatory fines. In some cases, an attacker can obtain a persistent backdoor into an organization's systems, 
leading to a long-term compromise that can go unnoticed for an extended period.


#### 🌴 How to detect SQL injection vulnerabilities:- 
SQL injection are detectable using a systematic set of tests against every entry point in the application. 
i) The single quote character ' and look for errors or other anomalies.
ii) Some SQL-specific syntax that evaluates to the base (original) value of the entry point, and to a different value, and look for systematic differences 
    in the application responses.
iii) Boolean conditions such as OR 1=1 and OR 1=2, and look for differences in the application's responses.
iv) Payloads designed to trigger time delays when executed within a SQL query, and look for differences in the time taken to respond.
v) OAST payloads designed to trigger an out-of-band network interaction when executed within a SQL query, and monitor any resulting interactions.


#### 🌴 SQL injection in different parts of the query:- 
