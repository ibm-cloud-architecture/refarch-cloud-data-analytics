<img src="./media/Step3-image-04.png" />

7. **Select** the **Manage** menu of the CDA Data Connect service on the left.
8. **Select** the **LAUNCH** button to launch the Data Connect service.

<img src="./media/Step3-image-05.png" />

9. **Select** the **X** in the top right corner of the Welcome dialog to close it.
10. **Select** the **Secure Gateway** menu from the Data Connect main menu on the left hand side.

<img src="./media/Step3-image-06.png" />

11. **Select** the **Add Gateway** button next to the moving arrow to add a gateway.

<img src="./media/Step3-image-07.png" />

12. **Enter** a gateway name of **Cloud-Data-Analytics**.
13. **Uncheck** the "Require security token to connect clients" check box.
14. **Uncheck** the "Token Expiration" check box.
15. **Select** the **Add Gateway** button.

<img src="./media/Step3-image-07-01.png" />

16. **Select** the **Settings** buton at the top of the page to view the Gateway settings.
17. **Select** the **Copy** button next to the Gateway ID to copy the Gateway ID to the clipboard. **Note -** this is a **very important** step because you are going to need this Gateway ID further on in the Prework to supply to the Secure Gateway client configuration file thta is installed on the VM image. Remember this ID or save it off so you can easily get back to it when its needed,
18. **Select** the **X** in the top right corner of the settings dialog to close the dialog.

<img src="./media/Step3-image-07-02.png" />

19. **Close** down the Data Connect service by selecting the **X** on the browser tab.

**Go Back** to your Bluemix Account for the next steps. 

<img src="./media/Step3-image-07-03.png" />

1. **Select** the "Catalog" menu at the top of the Bluemix home page.

<img src="./media/Step3-image-13.png" />

1. **Select** the **Manage** menu of the CDA dashDB service on the left.

<img src="./media/Step3-image-14.png"/>

2. **Select** the **OPEN** button to open the dashDB console.

<img src="./media/Step3-image-15.png"/>

3. **Select** the **Run SQL** menu from the left hand side of the console.

<img src="./media/Step3-image-16.png"/>

4. **Select** all the sample SQL in the SQL scratch pad area and delete it.

<img src="./media/Step3-image-17.png"/>

5. **Copy and Pate** the dashDB target table DDL from the [Bank Customers DDL File](https://github.com/ibm-cloud-architecture/refarch-cloud-data-analytics/blob/master/bank_customers.ddl).
6. **Select** the Run All button on the toolbar.

<img src="./media/Step3-image-18.png"/>

7. **Review** the results. It should complete successfully.
8. **Select** the **Tables** menu from the left hand side of the console.

<img src="./media/Step3-image-19.png"/>

9. **Select** the **BANK_CUSTOMERS** table from the tables drop down list box.

<img src="./media/Step3-image-20.png"/>

You will see the schema for the new table. The table is empty. You will be moving data from on-premies to this table in the move data to cloud excercies later on in this lab using Data Connect and optionally the Bluxemix Lift CLI.

# Prepare the Virtual Machine

## Steps
1. [Unzip the VM Image](#unzip)
1. [Power On the Virtual Machine](#power)
1. [Login to the Vritual Machine](#login)
1. [Update the Lift Properties File](#liftpf)
1. [Update the Secure Gateway ID](#secgwid)

<a name="unzip" />

## Unzip the VM Image

### On Windows

<img src="./media/vmimage/vmimage-image-01.png"/>

**Locate** the **Cloud Data Analytics.zip** VMWare Image zip file that you downloaded to your system in the Prework section.

**Unzip** the **Cloud Data Analytucs,zip** file using your favorite program of choice; 7 Zip,  WinZip etc.  It will create a **Cloud Data Analytics** folder into the location you choose to put it.

### On Mac OSX

<img src="./media/vmimage/vmimage-image-02.png"/>

**Locate** the **Cloud Data Analytics.zip** VMWare Image zip file that you downloaded to your system in the Prework section.

**Unzip** the **Cloud Data Analytucs,zip** file by simply **Double Click** the file or by selecting it, right mouse clicking and choosing to open it or open it using the Archive Utility. It will create a **Cloud Data Analytics** folder in the same location where the zip file resides and extract all the files into the folder.

<a name="power" />

## Power on the Virtual Machine

### On Windows

**VMWare Workstation**

<img src="./media/vmimage/vmimage-image-03.png"/>

**Open** the VMWare Workstation or VMWare Player application (you can use either or to open the VM).

1. **Select** the **File** menu from the toolbar.
2. **Select** the **Open** menu item.

<img src="./media/vmimage/vmimage-image-04.png"/>

3. **Go to** the location on your file system where you unzipped the VM Image.
4. **Select** the **NetezzaSoftwareEmulator.vmx** file.
5. **Select** the **Open** button.

<img src="./media/vmimage/vmimage-image-05.png"/>

6. **Select** the "Power on this virtual machine" button to Power on the Virtual Machine.

**VMWare Player**

<img src="./media/vmimage/vmimage-image-06.png"/>

1. **Select** the **Player** menu on the toolbar.
2. **Select** the **File** menu item.
3. **Select** the **Open** menu item.

<img src="./media/vmimage/vmimage-image-07.png"/>

4. **Go to** the location on your file system where you unzipped the VM Image.
5. **Select** the **NetezzaSoftwareEmulator.vmx** file.
6. **Select** the **Open** button.

<img src="./media/vmimage/vmimage-image-08.png"/>

7. **Select** the **Take Ownership** button when prompted.

<img src="./media/vmimage/vmimage-image-09.png"/>

8. **Select** the "Play Virtual Machine" button to Power on the virtual machine.

### On Mac OSX

<img src="./media/vmimage/vmimage-image-10.png"/>

**Open** the VMWare Fusion application (VMWare Player is not available for Mac OSX).

1. **Select** the **File** menu from the toolbar.
2. **Select** the **Open** menu item.

<img src="./media/vmimage/vmimage-image-11.png"/>

3. **Select** the **NetezzaSoftwareEmulator.vmx** file from within the **Cloud Data Analyitcs** VM Image folder.

<img src="./media/vmimage/vmimage-image-12.png"/>

4. **Select** the **Play** button to Power on the virtual machine.

<a name="login" />

## Login to the Virtual Machine

<a name="liftpf" />

## Update the Lift Properties

<a name="secgwid" />

## Update the Secure Gateway ID

Switch over to the VM an enter the following:
```
cd /etc/ibm
vi sgenvironment.conf
```
You now need to update the first line highlighted in red with your Gateway ID value.  Leave the `SECTOKEN` line as `none--`.
```
GATEWAY_ID="<your_gateway_id>"
```

![](/media/dataconnect/dc8a.png)

When finished, hold `SHIFT` and type `ZZ` to save and close the file.

Now we need to restart the secure gateway client.  One way to do that is to reboot the machine.  Using the VM Playr button, reboot the VM.

Back in your web browser, hit the X at the top-right of the popup to return to the Secure Gateway screen.  You should now see that 1 client is connected.
