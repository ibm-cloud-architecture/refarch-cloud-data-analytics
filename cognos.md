## Create a New data server Connection

Select Manage from the Navigation Panel. Hint : On the Bottom Left of the User Interface. 
Select Data Server Connection to create a new data server.

![](/media/CA/ca1.png)

Create a new data connection by selecting the ‘+’ and Select dashDB as the type

![](/media/CA/ca2.png)


![](/media/CA/ca3.png)
1. Rename the connection name from ‘New data server connection’ to ‘IA_Bank Customers’
1. Enter the your dashDB JDBC URL service credentials you obtained in the [prework exercise](https://github.com/ibm-cloud-architecture/refarch-cloud-data-analytics/blob/master/PreWork.md#step-d-create-the-dashdb-credentials).  Copy the "jdbcurl" (NOT the "ssljdbcurl") and paste into Cognos Analytics.  Your JDBC URL might look something like this (do not paste the quotes):  "jdbc:db2://dashdb-entry-yp-dal09-08.services.dal.bluemix.net:50000/BLUDB"
1. Create a signon associated to the new data connection. Select the ‘Use the following signon’ check box 
1. Select the  ‘+’ icon.

