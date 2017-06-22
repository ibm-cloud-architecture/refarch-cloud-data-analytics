# Configuring Data Connect

## Contents
1. [Launch the Data Connect service](#launch)
1. [Create and configure  the Secure Gateway](#creategw)
1. [Create the Connections](#createconn)
1. [Create the Data Movement Activity](#createact)
1. [Run Activity](#runact)

<a name="launch" /> 

## Launch the Data Connect service

In the Bluemix services screen, click on the CDA Data Connect service that you created.

![Services Screen](/media/dataconnect/dc0.png)


In the next screen, you will see a Launch button to access th Data Connect serice.

![Launch Data Connect](/media/dataconnect/dc1.png)

<a name="creategw" />

## Create and configure the Secure Gateway

The Secure Gateway is made up of a client-side component and a server-side service, which allows you to connect the Data Connect service to your virtual machine through a VPN tunnel. Typically, you would need to install the Secure Gateway client.  However, in the interest of time, this has already been downloaded and installed into the virtual machine.  The part that remains is to create the server-side service, and configure the client to connect to it.

Now that you are in the Data Connect screen, you will see a navigation pane on the left.  The first thing you need to do is create a Secure Gateway.  Click on Secure Gateway to create a direct connection into the virtual machine on your laptop.

![](/media/dataconnect/dc2.png)

Click the + button to create a new gateway

![](/media/dataconnect/dc4.png)

In the popup dialog, under "Add Gateway" enter the name: "Cloud-Data-Analytics"
You must uncheck the checkbox for "Require security token to connect clients"
Then, click Add Gateway

![](/media/dataconnect/dc5a.png)

Now that your secure gateway is created, we need the Gateway ID so that you can configure the client to use this new secure gateway.  Click on the Connect Client + button to see the Gateway ID.

![](/media/dataconnect/dc6.png)

In the popup, you can now see the Gateway ID.  In the free version of the VMware Player, it won't let you paste, so you'll need to enter this manually into a file in the VM.

![](/media/dataconnect/dc7.png)

Switch over to the VM and enter the following:
```
cd /etc/ibm
vi sgenvironment.conf
```
You now need to update the first line highlighted in red with your Gateway ID value.  Leave the `SECTOKEN` line as `none--`.
```
GATEWAY_ID="<your_gateway_id>"
```

![](/media/dataconnect/dc8.png)

When finished, hold `SHIFT` and type `ZZ` to save and close the file.

Now we need to restart the secure gateway client.  One way to do that is to reboot the machine.  Using the VM Playr button, reboot the VM.

Back in your web browser, hit the X at the top-right of the popup to return to the Secure Gateway screen.  You should now see that 1 client is connected.

<a name="createconn" />

## Create the Connections

In this step, you will configure 3 connections in Data Connect:
1. Connection to the PureData System for Analytics (PDA/Netezza) server in your VM
1. Connection to the DB2 server in your VM
1. Connection to the dashDB server that you created in your prework

To get started, click the Connections link on the navigation on the left (1).

![](/media/dataconnect/conn1.png)

### Connection to PDA.  

![](/media/dataconnect/conn2.png)

1. Click the Create New button at the top-right of the screen to create a new connection
1. In the list of connection types, select IBM PureData for Analytics

![](/media/dataconnect/conn3.png)

1. Name the connection "CDA PDA"
1. In the Hostname/IP Address field, enther the IP address that you saw when you first logged in to your VM.  If you did not write it down, you can type `ifconfig |head -2` to see it.  It should start with 192.168.
1. The port is 5480
1. The database name is BIDAY3
1. Ensure that "Use a secure gateway" is checked and then click the pull-down to select the gateway that you created in the prework.  It should be called "Cloud-Data-Analytics"
1. Enter the username "admin"
1. Enter the password "password"
1. Click the "Create Connection" button at the top-right of the screen

Now the PDA connection has ben created

### Connection to DB2

You will use the same steps as above for the DB2 connection, but with different values.

1. Click the Create New button at the top-right of the screen to create a new connection
1. In the list of connection types, select IBM DB2

![](/media/dataconnect/conn4.png)

1. Name the connection "CDA DB2"
1. In the Hostname/IP Address field, enther the IP address that you saw when you first logged in to your VM.  If you did not write it down, you can type `ifconfig |head -2` to see it.  It should start with 192.168.
1. The port is 50000
1. The database name is SAMPLE
1. Ensure that "Use a secure gateway" is checked and then click the pull-down to select the gateway that you created in the prework.  It should be called "Cloud-Data-Analytics"
1. Enter the username "db2inst1"
1. Enter the password "db2inst1"
1. Click the "Create Connection" button at the top-right of the screen

### Connection to dashDB

You will use the same steps as above for the dashDB connection, but with different values.

1. Enter a Connection Name of CDA dashDB
1. Click the Create New button at the top-right of the screen to create a new connection
1. In the list of connection types, select IBM dashDB
1. Enter the Host name from your dashDB service credentials you obtained in the prework exercise.
1. Enter a Database name of BLUDB – All dashDB plans use a database name of BLUDB.
1. Leave the Secure Gateway checkbox unchecked -- you do not need it for dashDB
1. Enter the Username from your dashDB service credentials you obtained in the prework exercise. 
1. Enter the Password from your dashDB service credentials you obtained in the prework exercise.
1. Select the Create Connection button. If successful, you will receive a message that “The connection CDA dashDB was created.”

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

![](/media/dataconnect/conn10.png)

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

1. In the resulting popup dialog, click on the text that says Coped to CDA dashDB

![](/media/dataconnect/conn17.png)

You will now see another popup.  Confirm that 11022 records were moved and take a screenshot for your records.
