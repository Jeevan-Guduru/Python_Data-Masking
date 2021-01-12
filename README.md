# Python_Data-Masking
This utility has been created as part of the data setup for Data engineering and analytical purposes.
More specifically, in lower environments - developement and testing , there is a requirement for building and testing the ETL jobs.
This activity requires data from various sources to be stored and manipulated in these environments which also may contain sensitive information of the customer like name,mobile number,address,banking information etc.
For security purposes , this data cannot be provided to testers or developers as is and should be protected. 
Data masking comes very handy for securing the sensitive information of customers.

#### About this utility ####
This is developed as part of the end to end automated Data masking tool building activity where user (tester/developer) will make a request from front end application which is built upon angular js . 

A request will contain the Source DB name, table/file name,schema of the source from where data has to be provided to the requested user's environment. Further, this request details are stored in the underlying DB (mySQL) in a table. 

Upon receiveing a request, this utility will connect to source DB using pre configured connection details and identifies the sensitive fields (Data Discovery) in the table/file mentioned in the request.

Once the senisitive fields are identified , appropriate masking functionality is applied on the data in that fields replacing the actual data.

Final output with masked data is sent to the target DB mentioned in the request.

==============================================================================================================================================================================
    Note : Functionality of the code in this repository pertains to Data masking of sensitive data which i have worked on and not end to end application. ==============================================================================================================================================================================


### Technical implementation ###

This utility is implemented in python in Jupyter notebook.
Pandas module is extensively used for data storing and manipulation.
Underlying Database used for this utility is mySQL DB.

###Metadata Tables:###



 <mark style="background-color: lightblue">tbl_data_request_hd</mark>- this is the table where the user request details are stored.

tbl_connection - this table has pre defined connection details to various DBs (configured with this utility) . This table can be updated from front end by admin whenever a new DB connection is required. 
Note : Each connection is identified by unique connection names which user can see and select in UI.

tbl_lookup - this is also pre-defined table which contains sensitive field names. This can also be updated from admin page as and when required.

tbl_data_discovery_hd - this table has the data with source name(file/table names) along with the sensitive fields in each source.
Data in this table is populated by dataDiscovery module, which matches the sensitive fields in the source data with above tbl_lookup and identifies sensitive fields in each source.

tbl_name_lookup - this table has mocked up data for first name , last name using which we create combinations of name data that is used to mask the actual names.

tbl_address_lookup - similar to names , this has mocked up address values , which is used to mask the actual addresses.

*****************************************************************************Work flow*************************************************************************************

1. User submits a request from front end UI with details of the data(schema,table/file names,source connection name,target connection name). This request details lands in request table - tbl_data_request_hd in mySQL DB
2. Masking_driver module fetches the request details - source name , source connection name and target connection name. 
3. Further it creates connection variable to source by reading connection details from tbl_connection using above connection name from request.
4. Then it calls data discovery module for identifying sensitive fields populating 'tbl_data_discovery_hd' table.
4. Later depending on the source type(file/table) it triggers correponding masking algorithms in fileMasking/tableMasking modules.
5. Finally masked data is loaded to underlying mySQL DB. 
Note: Masked data can be populated to target DB dynamically as per the input from user's request. However , this is still in development and we are not recieving the target DB details yet and for now we are storing the masked data in same MySQL Db where metadata is present.
******************************************************************************************************************************************************************************




