## Lab: Exploiting Unprotected Admin Functionality

### Steps

1. Open the lab and append `/robots.txt` to the lab URL.
     ![Webpage](https://github.com/asb1o8/WebSecurity_Labs/blob/main/Access%20Control/Img/webpage.png)
   

2. Check the `Disallow` entry to identify the disclosed admin panel path.
   
     ![Robot-file](https://github.com/asb1o8/WebSecurity_Labs/blob/main/Access%20Control/Img/robots.txt.png)
    
3. Replace `/robots.txt` in the URL with `/administrator-panel` to access the admin panel.

      ![Admin Panel](https://github.com/asb1o8/WebSecurity_Labs/blob/main/Access%20Control/Img/admin%20panel.png)

4. Locate the user **carlos** and delete the account.

     ![User Deleted](https://github.com/asb1o8/WebSecurity_Labs/blob/main/Access%20Control/Img/User%20deleted.png)


### Expected Result

The `robots.txt` file reveals the hidden administrative endpoint, which can be accessed without proper authorization.

**Conclusion:** The application has unprotected administrative functionality, resulting in vertical privilege escalation
