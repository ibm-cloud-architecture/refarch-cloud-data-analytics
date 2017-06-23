# Move Data to the Cloud using Data Connect

## Contents
1. [Launch the Data Connect service](#launch)
1. [Validate the Secure Gatway Client is Connected](#secgw)
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
1. **Enter** a port of **5000**.
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

Now that you have all the connections created, you can create an Activity which combines and moves the data from the PDA and DB2 sources and loads it into the dashDB target.

![](/media/dataconnect/conn5.png)

1. Click Activities on the navigation pane
1. Then, click the Create New button at the top-right of the screen

![](/media/dataconnect/conn6.png)

1. Move your mouse over Untitled Activity and then click the pencil icon to change the name of the Activity. Enter `CDA Move to Cloud` and then hit the Save button to the right of the text field.  You will then see the name of the Activity update.

![](/media/dataconnect/conn7.png)

Now we will select the tables that we want to copy.  

1. Click on CDA PDA
1. Click the ENABLEMENT schema
1. Check the box beside KBANK_CUSTOMERS to select the table
1. All of the columns will be automatically selected
1. Notice that the KBANK_CUSTOMERS is added to the Selected column

Next, we want to also select the DB2 table

![](/media/dataconnect/conn8.png)

1. Click on CDA DB2
1. Click the DB2INST1 schema
1. Check the box beside NBANK_CUSTOMERS to select the table
1. All of the columns will be automatically selected
1. Notice that the NBANK_CUSTOMERS is added to the Selected column, along with KBANK_CUSTOMERS which you added earlier
1. Click the Refine Data button so that we can combine the data

![](/media/dataconnect/conn9.png)

1. Click on Organize to expand the organize operations
1. Click on Union so that you can combine the data

![](/media/dataconnect/dc_goyti.png)

1. Check the NBANK_CUSTOMERS checkbox
1. Click the Apply button at the bottom
1. When that completes, click the Next button at the top-right

Now you can choose the target table.

![](/media/dataconnect/conn11.png)

1. Click CDA dashDB as the target connection
1. Select your schema (same as your userid from your dashDB service credentials you obtained in the prework exercise)
1. For the Table Action, select Replace the table contents
1. Click the pencil to edit the table name, and change it to BANK_CUSTOMERS, then click the green checkbox to save that name
1. Click the Save button to save the activity

<a name="runact" />

# Run the Activity

![](/media/dataconnect/conn12.png)

You should now see your new activity in the Activities dashboard.
Click the 3 dots to open the menu.

![](/media/dataconnect/conn13.png)

Click the Run icon and you will see a message saying "Your activity is running."
At the top-right of the screen, click the View Activity Status to monitor progress.
Click the refresh icon as indicated above to refresh the status.  Keep refreshing it until you see that it has completed 100%

![](/media/dataconnect/conn14.png)

When it has completed, click the X button beside the refresh button to close the status sidebar.

![](/media/dataconnect/conn15.png)

Click the 3 dots beside the activity again, to open the menu.
Click the Details button

![](/media/dataconnect/conn16.png)

In the resulting popup dialog, click on the text that says Copied to CDA dashDB (see *1*)

![](/media/dataconnect/conn17.png)

You will now see another popup.  Confirm that 11022 records were moved and take a screenshot for your records.
