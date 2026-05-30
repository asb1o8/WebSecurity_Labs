#### 🌴 IDOR:-
- A type of access control vulnerability that arises when an application uses user-supplied input to access objects directly.
- The term IDOR was popularized by its appearance in the OWASP 2007 Top Ten. However, it is just one example of many access control implementation mistakes that can lead to access controls being circumvented.
- IDOR vulnerabilities are most commonly associated with horizontal privilege escalation, but they can also arise in relation to vertical privilege escalation.


### 🌴 IDOR vulnerability with direct reference to database objects:

    https://insecure-website.com/customer_account?customer_number=132355

 - Here, the customer number is used directly as a record index in queries that are performed on the back-end database. If no other controls are in place, an attacker can 
 simply modify the `customer_number` value, bypassing access controls to view the records of other customers. This is an example of an IDOR vuln leading to horizontal 
 privilege escalation.

- An attacker might be able to perform horizontal & vertical privilege escalation by altering the user to one with additional privileges while bypassing access controls.
  Other possibilities include exploiting password leakage or modifying parameters once the attacker has landed in the user's accounts page, for example:-

  #### IDOR vulnerability with direct reference to static files:
- IDOR vulnerabilities often arise when sensitive resources are located in static files on the server-side filesystem. For example, a website might save chat message transcripts to disk using an *incrementing filename*, and allow users to retrieve these by visiting a URL like the following:

      https://insecure-website.com/static/12144.txt

- In this situation, an attacker can simply modify the filename to retrieve a transcript created by another user and potentially obtain user credentials and other sensitive data.
