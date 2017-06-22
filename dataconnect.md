# Configuring Data Connect

## Contents
1. [Launch the Data Connect service](#launch)
1. [Create and configure  the Secure Gateway](#creategw)
1. [Create Connections](#createconn)
1. [Create Activity](#createact)
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

## Create Connections

In this step, you will configure 3 connections in Data Connect:
1. Connection to the PureData System for Analytics (PDA/Netezza) server in your VM
1. Connection to the DB2 server in your VM
1. Connection to the dashDB server that you created in your prework

We will start with the connection to the PDA.
