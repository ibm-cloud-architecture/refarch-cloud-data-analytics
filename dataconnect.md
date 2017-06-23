# Move Data to the Cloud using Data Connect

## Contents
1. [Launch the Data Connect service](#launch)
1. [Validate the Secure Gateway Client is Connected](#secgw)
1. [Create the Source and Target Connections](#createconn)
1. [Create the Data Movement Activity](#createact)
1. [Run the Data Movement Activity](#runact)
1. [Validate the Data Movement Results](#validact)

<a name="launch" /> 

## Launch the Data Connect Service

<img src="./media/dataconnect/data-connect-image-01.png" />

1. **Click on** the **CDA Data Connect** service from your Bluemix Account services area.

<img src="./media/dataconnect/data-connect-image-02.png" />

2. **Select** the **LAUNCH** button to launch the Data Connect service. It will open up in a new tab in your browser.

<img src="./media/dataconnect/data-connect-image-03.png" />

3. **Select** the **X** in the top right corner of the Data Connect Welcome dialog to close the dialog.
4. **Select** the **Secure Gateway** menu from the Data Connect main menu on the left hand side.

<a name="secgw" />

## Validate the Secure Gateway Client Connection

<img src="./media/dataconnect/data-connect-image-04.png" />

You should see that you a Secure Gateway client is connected in the Secure Gateway client section as depicted above. There should also be a green client connection icon in the top right hand corner signifying that client(s) are connected and ready for work. 

> If your Secure Gatway section **does not** look like the screen shot above then your Secure Gateway client in the VM Image may not have the correct Gateway ID to communicate with your Data Connnect Secure Gateway. If that is the case, go back to the Prework section of this lab where you were instructed to configure the Secure Gateway client and make sure the Gateway ID is equal to the Gateway ID of your Secure Gateway. 

If everything is green, and you see that your Secure Gateway client is connected, proceed...

1. **Select** the **Data Connect** title in the top left corner of the service to go to the home page.

<a name="createconn" />

## Create the Source and Target Connections

In this step, you will create three Data Connect connections:

*dashDB for Analytics* - This is your target data souce where yo uwill move the DB2 and PDA on=premises data to
*PureData for Analytics* - This is the on-premises PDA database in the VM that contains K Bank's Customer data
*DB2 LUW* - This is the on-premises DB2 databae in the VM that contains N Banks"s Customer data

<img src="./media/dataconnect/data-connect-image-05.png" />

1. **Select** the **Connections** link in the middle of the Data Connect home page to begin creating connections.

### Create the dashDB for Analytics Connection  

<img src="./media/dataconnect/data-connect-image-06.png" />

1. **Select** the **IBM dashDB** connector from the list of connection types.

<img src="./media/dataconnect/data-connect-image-07.png" />

1. **Enter** a connect name of **CDA DASHDB**.
1. **Enter** a description of **CDA dashDB Database**.
1. **Enter** the host name from your dashDB service credentials.
1. **Enter** a Database name of **BLUDB** - All dashDB plans use a database name of BLUDB.
1. **Enter** the username from your dashDB service credentials.
1. **Enter** the password from your dashDB service credentials.
1. **Select** the **Create Connection** button.

### Create the DB2 Connection

<img src="./media/dataconnect/data-connect-image-08.png" />

1. **Select** the **Create New** button in the top right corner.

<img src="./media/dataconnect/data-connect-image-09.png" />

1. **Select** the **IBM DB2** connection from the list of connection types.

<img src="./media/dataconnect/data-connect-image-10.png" />

1. **Enter** a connect name of **CDA DB2**.
1. **Enter** a description of **CDA DB2 Database**.
1. **Enter** the **IP Address** of your VM Image as the host name.
1. **Enter** a port of **50000**.
1. **Enter** a Database of **SAMPLE**.
1. **Select** the Cloud-Data-Analytics secure gateway from the list. There should only be one.
1. **Enter** a username of **db2inst1**.
1. **Enter** a password of **db2inst1**.
1. **Select** the **Create Connection** button.

### Create the PureData for Analytics Connection

<img src="./media/dataconnect/data-connect-image-11.png" />

1. **Select** the **Create New** button in the top right corner.

<img src="./media/dataconnect/data-connect-image-12.png" />

1. **Select** the **IBM PureData for Analytics** connecter from the list of connection types.

<img src="./media/dataconnect/data-connect-image-13.png" />

1. **Enter** a connect name of **CDA PDA**.
1. **Enter** a description of **CDA PureData for Analytics Database**.
1. **Enter** the **IP Address** of your VM Image as the host name.
1. **Enter** a port of **5480**.
1. **Enter** a Database of **BIDAY3**.
1. **Select** your Cloud-Data-Analytics secure gateway from the list. There should only be one.
1. **Enter** a username of **admin**.
1. **Enter** a password of **password**.
1. **Select** the **Create Connection** button.

<a name="createact" />

## Create the Data Movement Activity

Now that you have all the connections created, you will create a Data Connect Activity which will read the K Bank Customers from PDA on-premies and the N Bank Customers from DB2 on-premises, combine the customers from both banks using a union, sort the data by Customer and then move the data to dashDB on the cloud.

<img src="./media/dataconnect/data-connect-image-14.png" />

1. **Select** the **Refine and Copy** menu item from the Data Connect main menu on the left.

<img src="./media/dataconnect/data-connect-image-15.png" />

1. **Select** the **Connections** category.
1. **Select** the **CDA DB2** connection from the list of connections.
1. **Select** the **DB2INST1** schema from the list of schemas.
1. **Select** the **NBANK_CUSTOMERS** table from the list of tables.

<img src="./media/dataconnect/data-connect-image-16.png" />

5. **Select** the **CDA PDA** connection from the list of connections.
6. **Select** the **ENABLEMENT** schema from the list of schemas.
7. **Select** the **KBANK_CUSTOMERS** table from the list of tables.

<img src="./media/dataconnect/data-connect-image-17.png" />

8. **Select** the edit icon next to the default "Untitled 1" activity name.

<img src="./media/dataconnect/data-connect-image-18.png" />

9. **Enter** an activty name of **CDA Move to Cloud**.
10. **Select** the **Save** button next to the name.

<img src="./media/dataconnect/data-connect-image-19.png" />

11. **Select** the **Refine Data** button to go into the Data Connect shaper.

<img src="./media/dataconnect/data-connect-image-20.png" />

1. **Select** the **Organize** category from the Operations side bar section on the right hand side.
1. **Select** the **Union** operation.

<img src="./media/dataconnect/data-connect-image-21.png" />

3. **Select** the **check box** next to the **KBANK_CUSTOMERS** table as the table to union.
4. **Select** the **Apply** button**.

<img src="./media/dataconnect/data-connect-image-22.png" />

5. **Select** the elippse in the right corner of the **Customer** column and then **Select** the **Sort Ascending** menu item.

<img src="./media/dataconnect/data-connect-image-23.png" />

6. **Select** the **Next** button in the top right corner.

<img src="./media/dataconnect/data-connect-image-24.png" />

7. **Select** the **CDA DASHDB** connection from the list of connetions.
8. **Select** the **DASH....** schema, your dashDB schema, from the list of schemas.
9. **Select** the **Replace table contents** radio button from the list of table actions. **Note -** This is an important step so make sure you select the correct table action. You want to replace the entire table contents.
10. **Select** the edit icon next to the **NBANK_CUSTOMERS** target table name to change the target table name.

<img src="./media/dataconnect/data-connect-image-25.png" />

11. **Enter** a target table name of **BANK_CUSTOMERS** for the target table name.
12. **Select** the green check mark next to the new target table name to save the name change. Your new target table name should now be **BANK_CUSTOMERS**.

<a name="runact" />

## Run the Data Movement Activity

<img src="./media/dataconnect/data-connect-image-26.png" />

1. **Select** the **Run** button in the top right corner of the shaper.

<img src="./media/dataconnect/data-connect-image-27.png" />

2. **Select** the **X** on the "Your activity is running" message to close the message.
3. **Select** the **View Activities Status** link to bring up the activity monitor.

<a name="validact" />

## Validate the Data Movement Results

<img src="./media/dataconnect/data-connect-image-28.png" />

1. **Select** the **Refresh** button on the activity status monitor to update the status.

> Keep hitting the **Refresh** button until you see a status of **Copied to** and **100% completed**.

2. **Select** the **Copied to** link in the status monitor for the activity to view the activity log.

<img src="./media/dataconnect/data-connect-image-29.png" />

> You should see that the number of **Records Moved** is equal to 11,022 rows.

3. **Select** the **X** in the top right corner of the activity log dialog to close the activity log dialog.

<img src="./media/dataconnect/data-connect-image-30.png" />

4. **Select** the **X** in the top right cornder of the activity status monitor to close the monitor.
5. **Seelect** the ellipse in the middle of the **CDA Move to Cloud** activity.
6. **Select** the **Details** option to view the activity details.

<img src="./media/dataconnect/data-connect-image-31.png" />

7. **Select** the **View data** link in the **OUTPUTS** section of the activity detail.

<img src="./media/dataconnect/data-connect-image-32.png" />

8. **Scroll** to the right to view all the columns.
9. **Scroll** down to view the 100 row sample set provided.
10. **Select** the **X** in the top right corner of the View data dialog to close the dialog.

Congratulations! You have successfully move data to the cloud using Data Connect.
