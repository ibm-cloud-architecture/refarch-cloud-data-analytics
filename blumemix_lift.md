Exercise 2: Prepare On-Premises

 	You should have already downloaded the PureData for Analytics Virtual Machine Simulator image for your workstation operating system. If you have not, go back to the Workflow section and click on the link to download the VM zip file.

Step 1: Extract the Archive

 

1.	Locate the NetezzaSoftwareEmulator_7.2.1_Lift.zip file that you just downloaded to your file system.
2.	Extract the contents to your desired location using the archive extraction software of your choice.

Step 2: Prepare the Virtual Machine

Open your VMWare Workstation on your respective workstation. Note – I do not have a Mac with VMWare Fusion so these examples are using VMWare on Windows. However, the process will be similar on Mac OSX.

 

3.	Select the “File” menu on the toolbar.
4.	Select the “Open…” menu item.

 

5.	Go to the folder where you extracted the Lift Netezza Software Emulator zip file.
6.	Select the NetezzaSoftwareEmulator.vmx file.
7.	Select the Open button.

 

8.	Select the Power on this virtual machine button.
 

9.	Select the I copied it button when prompted if the virtual machine has been moved or copied. This will give you a new virtual IP address for this virtual machine.

Step 3: Login to the Virtual Machine

The credentials for this Virtual Machine are as follows:

Root = root / netezza
Netezza User = nz / nz – You will use these credentials to log into the VM.
Netezza Admin = admin / password – You will use these credentials for your Lift migration.

 

1.	Enter a login id of nz and a password of nz. The Virtual Machine’s IP Address is displayed.
2.	Enter the command ls -la and press enter to get a list of directories and files.

You will see the Lift CLI zip file, lift-cli-linux.zip, and a directory, lift-cli-data. The data directory was created for you and will be where you will place the CSV file for the NZ_WEB_SALES table that will be created when you extract the data from the ENABLEMENT.NZ_WEB_SALES table in the BIDAY3 database. The lift-cli-data directory contains two Lift properties files, that were created for you, that contain the source and target parameters that will be used by the Lift CLI. Lift allows you to designate a “property” file that contains command line options so you don’t have to provide them on the command line. You will edit the dashDB properties file to supply your dashDB service information. The path to the Lift CLI bin directory export/home/nz/lift-cli/bin has been added to the nz users path using a PATH statement in the .bashrc file.

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

