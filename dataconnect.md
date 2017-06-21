# Configuring Data Connect

## Contents
1. Launch the Data Connect service
1. Create and configure  the Secure Gateway
1. Create Connections
1. Create Activity
1. Run Activity

## Launch the Data Connect service
In the Bluemix services screen, click on the CDA Data Connect service that you created.

![Services Screen](/media/dataconnect/dc0.png)


In the next screen, you will see a Launch button to access th Data Connect serice.

![Launch Data Connect](/media/dataconnect/dc1.png)

## Create and configure the Secure Gateway
The Secure Gateway is made up of a client-side component and a server-side service, which allows you to connect the Data Connect service to your virtual machine through a VPN tunnel. Typically, you would need to install the Secure Gateway client.  However, in the interest of time, this has already been downloaded and installed into the virtual machine.  The part that remains is to create the server-side service, and configure the client to connect to it.

Now that you are in the Data Connect screen, you will see a navigation pane on the left.  The first thing you need to do is create a Secure Gateway.  Click on Secure Gateway to create a direct connection into the virtual machine on your laptop.

![](/media/dataconnect/dc2.png)

Click the + button to create a new gateway

![](/media/dataconnect/dc4.png)

In the popup dialog, under "Add Gateway" enter the name: "Cloud-Data-Analytics"
Leave the two Token checkboxes checked
Then, click Add Gateway

![](/media/dataconnect/dc5.png)

Now that your secure gateway is created, we need to find out the Gateway ID and Security Token so that you can configure the client to use this new secure gateway.  Click on the Connect Client + button to see these unique identifiers.

![](/media/dataconnect/dc6.png)

In the popup, you can now see the Gateway ID and the Security Token.  You'll need to copy each of these into a file in the VM.  To do that, start with the Gateway ID.  Click on the copy button beside the Gateway ID, highlighted in the left red box below.

![](/media/dataconnect/dc7.png)

With the Gateway ID in the clipboard, switch over to the VM and enter the following:
``` cd /etc/ibm
vi sgenvironment.conf ```

You now need to update the two lines highlighted in red:
``` GATEWAY_ID="<your_gateway_id>"
SECTOKEN="<your_security_token>" ```

