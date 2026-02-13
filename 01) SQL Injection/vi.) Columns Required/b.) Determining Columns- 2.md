##  ⛳ Determining the number of columns required- 2

- The second method involves submitting a series of `UNION SELECT` payloads specifying a different number of null 
  values:
  
     ' UNION SELECT NULL--
     ' UNION SELECT NULL,NULL--
     ' UNION SELECT NULL,NULL,NULL--
       etc.

