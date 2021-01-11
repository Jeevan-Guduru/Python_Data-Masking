# Python_Data-Masking
This utility has been created as part of the data setup for Data engineering and analytical purposes.
More specifically, in lower environments - developement and testing , there is a requirement for building and testing the ETL jobs.
This activity requires data from various sources to be stored and manipulated in these environments which also may contain sensitive information of the customer like name,mobile number,address,banking information etc.
For security purposes , this data cannot be provided to testers or developers as is and should be protected. 
Data masking comes very handy for securing the sensitive information of customers.

#### About this utility ####
This is developed as part of the end to end automated Data masking tool building activity where user (tester/developer) will make a request from front end application which is built upon angular js . 

A request will contain the Source DB name, table/file name,schema of the source from where data has to be provided to the requested user's environment. Further, this request details are stored in the underlying DB (mySQL) in a table. 

Upon receiveing a request, this utility will connect to source DB and identifies the sensitive fields (Data Discovery) from the table/file in the request.

Once the senisitive fields are identified , appropriate masking functionality is applied on the data in that fields replacing the actual data.

Final output with masked data is sent to the target DB mentioned in the request.

Note : Here am placing the backend functionality (data discovery and masking) which i have developed and not end to end applicaiton.


