# Moving data and workloads from on-premises to the Cloud for more agile analytics

- **[Introduction](#introduction)**
- **[Narrative](#narrative)**
- **[Solution Overview](#solution-overview)**
- **[Solution Components & Services](#solution-components-and-services)**
- **[Prerequisites](#prerequisites)**

**The main part of the lab starts here**

- **[Move the Data to the Cloud](#move-the-data-to-the-cloud)**
    - [Step 1: Create the Cloud Data Analytics lab services](#step-1-create-the-cloud-data-analytics-lab-services)
    - [Step 2: Create the dashDB Credentials](#step-2-create-the-dashdb-credentials)
    - [Step 3: Work with the VM](#step-3-work-with-the-vm)
        - [Step 3a: Set the Keyboard](#step-3a-set-the-keyboard)
    - [Step 4: Update the Secure Gateway ID](#step-4-update-the-secure-gateway-id)
    - [Step 5: Move Data to the Cloud using Data Connect](#step-5-move-data-to-the-cloud-using-data-connect)

- **[Analyze the Data](#analyze-the-data)**
    - [Step 1: Setup Cognos](#step-1-setup-cognos) 
    - [Step 2: Getting Insight](#step-2-getting-insight) 

# Introduction

This project provides a reference implementation for moving data from on-premises relational database(s) into a Cloud Managed Database Service (dashDB) so that the data can be analyzed quickly, easily, and without the need to setup any new hardware or request resources from the IT department. In this example, the on-premises databases are in two different RDBMS'es to emulate two different organizations. However, you could use a similar pattern and set of steps to copy from a single database into the cloud as well. 

In this case, one organization is using IBM's PureData System for Analytics (Netezza) and the other Db2 on Linux for their data warehouses. The data from these systems will be pushed into dashDB in the cloud so that it can be combined and analyzed as a single entity.  

**We will provide two mechanisms for moving the data from on-premises to the cloud, Bluemix Data Connect and Lift CLI, so that you can choose the method based on who you are demoing to.** Data Connect is a cleaner, easier solution for one time moves, and best used when demoing to Business Users (LOB managers and executives). Lift CLI is how we would productionalize the initial and delta data load process, and best used when demoing to IT.

### Loading data using IBM Data Connect

![Overview](Images/SystemOverviewConnect2.png)

### Loading data using IBM Bluemix Lift CLI

![Overview](Images/SystemOverviewLift1.png)

# Narrative 

Consider the following scenario: You are talking to the Chief Marketing Officer (CMO) at "K Bank". 

In this lab we used the scenario/narrative below, but here is a [video](https://github.com/ibm-cloud-architecture/refarch-cloud-data-analytics/blob/master/InternDemoIntro.mov) of one of IBM's Technical Sales Interns presenting the same solution with a couple other ways to look at the data once it is combined to show that this use case can open up so many new opportunities. 

## Lab Narrative

Hi Ms. Smith, I know that "K Bank" just bought "N Bank". I just came from a meeting on how you plan to integrate the two companies’ systems and it is going to take quite a while. I would think that many people, and you in particular, can’t wait for a year or more for the integrated data to start reaching out to your customers.

I know that "K Bank" has been doing churn analytics for some time, but the team at "N Bank" has not. "K Bank" has found that customer loss (churn) is directly related to the customer's satisfaction level. This is kind of obvious, so it would be interesting to see how these churn prediction models could be used to look at "N Bank" customers and identify who might be at risk of leaving. Since "K Bank" just spent a lot of money to acquire "N Bank", you do not want to lose any customers if you can help it.  

IBM can help you combine the data from both banks now, so that you can get access to this combined data within days, without putting any load on your IT staff who is already overloaded with the consolidation.  We can use IBM's fully managed cloud services to copy data from your current on-premises systems in each bank into a cloud data warehouse and give you a single view of your customers across both banks.
 
Once you have that data at your fingertips, you can explore the data and discover how satisfied your customers are, within each Bank and across both Banks. You can also identify which customers are leaving the bank and which ones you should strive to retain.

We can quickly show you how to create a dashboard to showcase your findings, use it to tell a story of what you discovered and the actions you might want to take base on this analysis.

# Solution Overview

The solution is a Business Inteligence (BI) tool that allow Business Users to get quick but important insights from the data. In order to gain this insight the data from both bank systems need to be moved from their data centers into a common repository. Because IT cannot support creating and managing a new system and moving the data, the new, common repository needs to be hosted as a managed cloud service. The BI tools will then be connected to this new repository and the existing analytical reports will be run. 

# Solution Components and Services

There are a few components of this solution. We used a VM to emulate the on-premises systems, PureData System for Analytics (Netezza) and Db2. Both of these systems are commonly used by financial firms due to the performance and security they provide - not only for data at rest, but also data as it is being queried.   

We chose dashDB for Analytics (to be renamed **Db2 Warehouse on Cloud** as of ~July 18th) as the combined repository since it is a fully managed service in the cloud that can be expanded easily, needs no administration, and has built-in encryption and security. **Note** - dashDB is ISO 27001, SOC 2, SOC 3 and HIPAA certified. 

Data Connect uses the Secure Gateway to encrypt the data on the wire and Lift uses Aspera to transfer the data using very high levels of compression as well as automatic encryption.   

Cognos Analytics is a modern, self-service Business Intelligence Platform that provides a sleek and intuitive user experience. Cognos Analytics provides the ability to empower everyone in the organization to find insight from their data to positively impact their decision making.


# Prerequisites

You will need the following:

 - VMware
      - VMware Player or VMware Workstation for Windows
      - VMware Fusion (Full or 30 day trial) for OSX
 - The Virtual Machine (VM) for the lab
      - Download the [VMware Image](https://ibm.box.com/s/50uj4kfg87qe3rd3icjfvlx94xaygdmr) 
      
        > 
        > **Note**  
        >
        > The image download is 11 GB -- make sure you have a reliable high speed network to download this file! When unzipped the VMware image will consume 20GB of local disk (and up to 20GB temp space), and 3GB RAM. Users with limited RAM (8GB) will want to shut down as many applications as possible prior to launching VMware.
        > 
        
 - A Bluemix account
 - A provisioned Data Connect Starter service in Bluemix
 - A provisioned dashDB for Analytics (**Db2 Warehouse on Cloud** *as of ~July 18*) Entry service in Bluemix
 - dashDB access credentials
 - A Cognos Anlaytics Trial

> **Note**  
> 
> If you need help with any of the prerequisites, go to the [Prerequisite Step by Step Directions](https://github.com/ibm-cloud-architecture/refarch-cloud-data-analytics/blob/master/PreWork.md) page


# Move the Data to the Cloud

## Step 1: Create the Cloud Data Analytics Lab Services

<img src="./media/Step3-image-01.png" />

1. **Select** the **Catalog** menu at the top of the Bluemix home page.

<img src="./media/Step3-image-02.png" />

2. **Enter** "data connect" (without quotes) in the catalog search area to find the service faster than scrolling.  

3. **Click** on the “Data Connect” service.  

<img src="./media/Step3-image-03.png" />

4. **Enter** "CDA Data Connect” (without quotes) for the Service name.  (We are using CDA as the short form for Cloud-Data-Analytics).

5. **Enter** “CDA Data Connect” (without quotes) for the Credential name.  

6. **Click** on the the "Create" button. The service will be created and the launch page is displayed.

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

16. **Select** the **Settings** button (the gear icon) at the top of the page to view the Gateway settings.

17. **Select** the gateway ID, Copy and save it - you will need it later.  

> **Note -** 
>
> This is a **very important** step because you are going to need this Gateway ID further on in the pre-work to supply to the Secure Gateway client configuration file that is installed on the VM image. Remember this ID or save it off so you can easily get back to it when it's needed.

18. **Select** the **X** in the top right corner of the settings dialog to close the dialog.

<img src="./media/Step3-image-07-02.png" />

19. **Close** down the Data Connect service browser tab by selecting the **X** on the browser tab.

**Go Back** to your Bluemix Account for the next steps. 

<img src="./media/Step3-image-07-03.png" />

1. **Select** the "Catalog" menu at the top of the Bluemix home page. 

<img src="./media/Step3-image-08.png" />

2. **Enter** "dashdb" (without quotes) in the catalog search area.  

3. **Click on** the “dashDB for Analytics” service.  

<img src="./media/Step3-image-09.png" />

4. **Enter** "CDA dashDB” (without quotes) for the Service name.   

5. **Select** the the "Create" button. The service will be created and the launch page is displayed.

<img src="./media/Step3-image-10.png" />

6. **Click On** the "CDA dashDB" service you just created from the list of services.


## Step 2: Create the dashDB Credentials


<img src="./media/Step3-image-10-1.png" >

7. **Select** the "Service credentials” section of the "CDA dashDB" service launch page.   

8. **Select** the the "New credential +" button.

<img src="./media/Step3-image-11.png" />

9. **Enter** "CDA dashDB” (without quotes) for the credential name.   

10. **Select** the the "Add" button. The service credential will be created.

<img src="./media/Step3-image-12.png" />

11. **Select** the "View credentials" down arrow to view the newly created credentials.

> **Note - **
> 
> These are the "CDA dashDB" service credentials you will need to access the dashDB service later when moving the data to the cloud. Copy all of this to the same place you saved the Data Connect Gateway ID you saved earlier. I have redacted my password to protect my identity. Yours will be visible.

<img src="./media/Step3-image-14.png"/>

1. **Select** the **Manage** menu of the CDA dashDB service on the left.

2. **Select** the **OPEN** button on the top right or under the "Where to Start" section at the bottom of the page to open the dashDB console.

<img src="./media/Step3-image-15.png"/>

3. **Select** the **Run SQL** menu from the left hand side of the console.

<img src="./media/Step3-image-16.png"/>

4. **Select** all the sample SQL in the SQL scratch pad area and delete it.

<img src="./media/Step3-image-17.png"/>

5. **Copy and Paste** the dashDB target table DDL from the [Bank Customers DDL File](https://github.com/ibm-cloud-architecture/refarch-cloud-data-analytics/blob/master/bank_customers.ddl).

6. **Select** the Run All button on the toolbar.

<img src="./media/Step3-image-18.png"/>

7. **Review** the results. It should complete successfully.

8. **Select** the **Tables** menu from the left hand side of the console.

<img src="./media/Step3-image-19.png"/>

9. **Select** the **BANK_CUSTOMERS** table from the tables drop down list box.

<img src="./media/Step3-image-20.png"/>

You will see the schema for the new table. The table is empty. You will be moving data from on-premises to this table in the move data to cloud exercises later on in this lab using Data Connect and optionally the Bluxemix Lift CLI.


# Work on the "On-Premises" Systems

> **NOTE -** 
>
> We use a VM with a running Db2 and PureData System for Analytics (Netezza) solution in it.  In reality these would likely be 2 separate systems, in different data centers, but this still represents that environment in a realistic manner.
>  

## Step 3: Work with the VM

## Steps

1. [Unzip the VM Image](#unzip)

1. [Power On the Virtual Machine](#power)

1. [Login to the Virtual Machine](#login)

1. [Update the Lift Properties File](#liftpf)

1. [Update the Secure Gateway ID](#secgwid)

<a name="unzip" />

## Unzip the VM Image

### On Windows

<img src="./media/vmimage/vmimage-image-01.png"/>

**Locate** the **Cloud Data Analytics.zip** VMWare Image zip file that you downloaded to your system in the Prework section.


### On Windows

**Unzip** the **Cloud Data Analytics.zip** file using your favorite program of choice; 7 Zip,  WinZip etc.  It will create a **Cloud Data Analytics** folder in the location you choose to put it.

### On Mac OSX

<img src="./media/vmimage/vmimage-image-02.png"/>

**Locate** the **Cloud Data Analytics.zip** VMWare Image zip file that you downloaded to your system in the Prework section.

**Unzip** the **Cloud Data Analytics.zip** file by simply **Double Clicking** the file or by selecting it, right mouse clicking and choosing to open it or open it using the Archive Utility. It will create a **Cloud Data Analytics** folder in the same location where the zip file resides and extract all the files into that folder.

<a name="power" />

## Power on the Virtual Machine

### On Windows

**VMWare Workstation**

<img src="./media/vmimage/vmimage-image-03.png"/>

**Open** the VMWare Workstation or VMWare Workstation Player application (you can use either or to open the VM).

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

<img src="./media/vmimage/VM-Move.png"/>

5. **Select** the **I Moved It** button so that the system maintains the configuration as we defined it.

<a name="login" />


### Note

>
> When you start working in the VM, your keyboard and mouse will be connected to the VM. You cannot just move the mouse outside the VM window to work on other applications. To **release** the mouse and keyboard from the VM, 
>
> On Windows hit CTL+ALT
>
> On Mac OSX hit control+command
>


## Virtual Machine Credentials

The credentials (userid / password) for this Virtual Machine (VM) are as follows:

- Root = root / netezza

- Netezza User = nz / nz – You will use these credentials to log into the VM

- Netezza Admin = admin / password – You will use these credentials for your Lift data migration


> **Note -** 
>
> Only do step 3A if you are NOT using a QWERTY keyboard layout
>


### Step 3a: Set the Keyboard

**OPTIONAL**  For a non QWERTY keyboard you likely will want to switch to a local keyboard to make the work easier.

[Instructions](https://github.com/ibm-cloud-architecture/refarch-cloud-data-analytics/blob/master/UpdateKeyboard.md)


## Login to the Virtual Machine

<img src="./media/vmimage/vmimage-image-13.png"/>

1. **Enter** a lowercase login id of **nz** and a password of **nz**. The Virtual Machine’s IP Address is displayed. Record this IP Address for use later on.

<a name="liftpf" />

<img src="./media/vmimage/vmimage-image-14.png"/>

## Step 4: Update the Secure Gateway ID

> In this section we will be editting some files. If you use **vi** directly in the VM, you cannot cut and paste. If you use the **ssh** command from your laptop into the VM you can cut and paste and eliminate a lot of manual typing complex strings.

<img src="./media/vmimage/SSH1.png"/>

Open a Terminal in Mac/OSX and enter the command **ssh nz@"your VM IP Address"**

When prompted "Are you sure you want to continue connecting (yes/no)?" - Type **yes**

Hit **Enter**

When prompted for the password, enter the password (nz) 

Hit **Enter**


> NOTE - 
>
> In Windows you will need Putty to do this. You can connect Putty to the IP Address in a similar fashion.
> 


<img src="./media/vmimage/vmimage-image-18.png"/>

1. **Enter** a command of **cd /etc/ibm**.

<img src="./media/vmimage/vmimage-image-19.png"/>

2. **Enter** a command of **ls**.

3. **Enter** a command of **vi sgenvironment.conf**.

<img src="./media/vmimage/vmimage-image-20.png"/>

**Note -** The GATEWAY_ID you will be changing is case sensitve so make sure you type it in exactly as it appears.

4. **Change** the **GATEWAY_ID**, to **GATEWAY_ID="<your_gateway_id>"**. This is your Data Connect service Secure Gateway ID that you were instructed to copy to the clipboard and save off.

5.	**When finished**, hold `SHIFT` and type `ZZ` to save and close the file.

<img src="./media/vmimage/vmimage-image-21.png"/>

6. **Enter** the command **reboot** to recycle the VM image. This will ensure that the Secure Gateway Client restarts and that it picks up your Gateway ID to communicate with your Data Connect service in the cloud.

<img src="./media/vmimage/vmimage-image-22.png"/>

7. **Enter** a lowercase login id of **nz** and a password of **nz** to log back into the VM image.

<img src="./media/vmimage/vmimage-image-23.png"/>

8. **Enter** the command **cd $DATA** to position yourself in the Lift CLI data directory.

## Step 5: Move Data to the Cloud using Data Connect

### Steps 
1. [Launch the Data Connect service](#launch)
1. [Validate the Secure Gateway Client is Connected](#secgw)
1. [Create the Source and Target Connections](#createconn)
1. [Create the Data Movement Activity](#createact)
1. [Run the Data Movement Activity](#runact)
1. [Validate the Data Movement Results](#validact)

Open a browser, go to bluemix.net, and log in. You will see the Welcome screen that looks like 

<img src="./media/dataconnect/WelcomeApps.png" />

Scroll down the screen until you see the list of all of your services, like shown below. 

<a name="launch" /> 

## Launch the Data Connect Service

<img src="./media/dataconnect/data-connect-image-01.png" />

1. **Click on** the **CDA Data Connect** service from your Bluemix Account services area.

<img src="./media/dataconnect/data-connect-image-02.png" />

2. **Select** the **LAUNCH** button to launch the Data Connect service. It will open up in a new tab in your browser.

<img src="./media/dataconnect/data-connect-image-03.png" />

3. If you get the Welcome screen, **Select** the **X** in the top right corner of the Data Connect Welcome dialog to close the dialog.

4. **Select** the **Secure Gateway** menu from the Data Connect main menu on the left hand side.

<a name="secgw" />

## Validate the Secure Gateway Client is Connected

> **PLEASE NOTE**
> 
> The Secure Gateway Interface changed slightly. You now need to select the grey box for the connection to check its status. 

<img src="./media/dataconnect/data-connect-image-04b.png" />

Click on the grey box for your gateway.

<img src="./media/dataconnect/data-connect-image-04.png" />

You should see that your Secure Gateway client is connected in the Secure Gateway client section as depicted above. There should also be a green client connection icon in the top right hand corner signifying that client(s) are connected and ready for work. 

> **BE CAREFUL**
> 
> If your Secure Gateway section **does not** look like the screen shot above - then your Secure Gateway client in the VM Image may not have the correct Gateway ID to communicate with your Data Connnect Secure Gateway. If that is the case, go back to the [Create the Cloud Data Analytics lab services](#step-1-create-the-cloud-data-analytics-lab-services) section of this lab where you were instructed to configure the Secure Gateway client and make sure the Gateway ID is equal to the Gateway ID of your Secure Gateway. 
> 

When everything is green, and you see that your Secure Gateway client is connected, proceed.

1. **Select** the **Data Connect** title in the top left corner of the service to go to the home page.

<a name="createconn" />

## Create the Source and Target Connections

In this step, you will create three Data Connect connections:

1. dashDB for Analytics - This is your target data source where you will move the Db2 and PDA on-premises data to

1. PureData for Analytics - This is the on-premises PDA database in the VM that contains K Bank's Customer data

1. Db2 - This is the on-premises Db2 database in the VM that contains N Banks's Customer data

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

### Create the Db2 Connection

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

Now that you have all the connections created, you will create a Data Connect Activity which will read the K Bank Customers from PDA on-premises and the N Bank Customers from Db2 on-premises, combine the customers from both banks using a union, sort the data by Customer and then move the data to dashDB on the cloud.

<img src="./media/dataconnect/data-connect-image-14.png" />

1. **Select** the **Refine and Copy** menu item from the Data Connect main menu on the left.

<img src="./media/dataconnect/data-connect-image-15.png" />

1. **Select** the **Connections** category.

1. **Select** the **CDA DB2** connection from the list of connections.

1. **Select** the **DB2INST1** schema from the list of schemas.

1. **Click** the check box beside the **NBANK_CUSTOMERS** table in the list of tables.

<img src="./media/dataconnect/data-connect-image-16.png" />

5. **Select** the **CDA PDA** connection from the list of connections.

6. **Select** the **ENABLEMENT** schema from the list of schemas.

7. **Click** the check box beside the **KBANK_CUSTOMERS** table in the list of tables.

<img src="./media/dataconnect/data-connect-image-17.png" />

8. **Select** the edit icon (the pencil) next to the default "Untitled 1" activity name.

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

5. Hover over the customer column and then **Select** the three dots the right corner of the **Customer** column and then **Select** the **Sort Ascending** menu item.

<img src="./media/dataconnect/data-connect-image-23.png" />

6. **Select** the **Next** button in the top right corner.

<img src="./media/dataconnect/data-connect-image-24.png" />

7. **Select** the **CDA DASHDB** connection from the list of connections.

8. **Select** the **DASH####** schema (your dashDB schema) from the list of schemas.

9. **Select** the **Replace the table contents** radio button from the list of table actions. 

> **Note -** 
> 
> This is an important step so make sure you select the correct table action. You want to replace the entire table contents.


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

5. **Select** the three dots on the top right of the **CDA Move to Cloud** activity.

6. **Select** the **Details** option to view the activity details.

<img src="./media/dataconnect/data-connect-image-31.png" />

7. **Select** the **View data** link in the **OUTPUTS** section of the activity detail.

<img src="./media/dataconnect/data-connect-image-32.png" />

8. **Scroll** to the right to view all the columns.

9. **Scroll** down to view the 100 row sample set provided.

10. **Select** the **X** in the top right corner of the View data dialog to close the dialog.

Congratulations! You have successfully moved data to the cloud using Data Connect.

> ____________________________________________________________________________________ 
>
>
> **Note:**
>    
>  
> If you want to try to move the data again using the Lift CLI, go to [Lift4Move.md](https://github.com/ibm-cloud-architecture/refarch-cloud-data-analytics/blob/master/Lift4Move.md)
>  
>  
> ____________________________________________________________________________________ 


# Analyze the Data


## Step 1: Setup Cognos


[Click Here to Go to Cognos Analytics on Cloud](https://www.ibm.com/analytics/us/en/technology/products/cognos-analytics/)


<img src="./cmedia/ca-image-01.png" >

1. **Select** the **Sign In** button in the top right corner.

<img src="./cmedia/ca-image-02.png" >

2. **Enter** your IBM Account.

**Note -** Cognos Analytics on Cloud checks if the IBM account entered is associated with an IBM w3ID. If you are an IBM employee with a w3ID, complete the login process using section [Authenticate uisng your IBM w3ID](#w3). Otherwise, continue with step 3 and 4 below.

>  **
> Using Safari on Mac OSX we have had some people have their w3ID signon continue to loop.  
> The development team is working this.
> If you encounter this the easiest solution is to try a different browser, such as Firefox
> **

<img src="./cmedia/ca-image-03.png" >

3. **Enter** your IBM Account **password**.

4. **Select** the **Log in** button.


<img src="./cmedia/ca-image-07.png" >


You are brought to the Cognos Analytics on Cloud home page.

<a name="w3" />

### Authenticate using your IBM w3ID


<img src="./cmedia/ca-image-04.png" >


1. **Select** the **Continue** button to gain access to IBM Cognos Analytics on Cloud using your IBM w3ID.


<img src="./cmedia/ca-image-05.png" >


2. **Enter** your **w3ID** and **password**

3. **Select** the **Sign In** button.


<img src="./cmedia/ca-image-06.png" >


4. **Check or Uncheck** the checkbox depending your choice of being informed of IBM products....

5. **Select** the **Continue** button.


<img src="./cmedia/ca-image-07.png" >


You are brought to the Cognos Analytics on Cloud home page.


### Create a Data server connection

Before you bein, **Go Back** to your Bluemix account. **Click on** your dashDB service from the service dashboard and go to your dashDB service credentials section that you created in the PreWork section. 


<img src="./cmedia/ca-image-10.png" >


You will need the **jdbcurl**, **username** and **password** from the credentials section of the service to complete the creation of your data server connection in the following steps. Leave this open in your browser so you can copy and paste from it to complete the creation of the data server connection section. 


**Go Back** to the Cogons Analytics on Cloud application in your browser. 


<img src="./cmedia/ca-image-08.png" >


1. **Select** the **Manage** button on the bottom left side of the home page.

2. **Select** the **Data server connections** menu item to create a new data server connection.


<img src="./cmedia/ca-image-09.png" >


3. **Select** the **+ plus sign** to create a new connection.

4. **Select** a type of **dashDB**.


<img src="./cmedia/ca-image-11.png" >


**Note -** A Data Server connection name has to be unique across the Cognos Analytics for Cloud shared environment. Therefore, you will use your dashDB username from your dashDB service credentials plus "Bank Customers" to make the name unique. For instance, my Data Server connection name will be **dash13919 Bank Customers**.


5. **Select** the **edit** icon that looks like a pencil next to the "New data server connection" name. **Enter** a name of **dash13919 Bank Customers** (your dashDB username of your dashDB service + Bank Customers) and **click** outside the edit area to save the name.

6. **Copy and Paste** the **jdbcurl** from your dashDB service credentials section into the data connection JDBC URL text box.

> Your JDBC URL will look like this: **jdbc:db2://dashdb-entry-yp-dal09-08.services.dal.bluemix.net:50000/BLUDB**

7. **Select** the **Use the following signon** radio button.

8. **Select** the **+ plus sign** right next to the drop down list box of signons.

<img src="./cmedia/ca-image-12.png" >

9. **Enter or Copy & Paste** your dashDB **username** from your dashDB credentials into the User ID field.

10. **Enter or Copy & Paste** your dashDB **password** from your dashDB credentials into the Password field.

11. **Enter or Copy & Paste** your dashDB **password** from your dashDB credentials into the Confirm Password field.

12. **Select** the **Test** button to test the connection.

The **Test** should succeeed and you will see a **Success** status with a green check mark next to it. If not, go back and double check your JDBC URL, User ID and password and make sure you entered then correctly and retry the test.

13. **Select** the **Save** button to save your dashDB data connection. 

Now you will **select** the database schema that you will use in this exercise. 

<img src="./cmedia/ca-image-13.png" >

1. **Select** the **Schemas** tab of your **dashXXXXX Bank Customers** data server connection.

2. **Click on** the **ellipse** ... on the schema that is associated to your dashDB username.

3. **Select** the **Load metadata** menu item.

<img src="./cmedia/ca-image-14.png" >

When the schema is successfully loaded, the status column next to the schema name will have a green check mark.

### Create a Data Module

With Cognos Analytics, users are not restricted to only using existing enterprise data sources. Users can blend personal data or external data with enterprise data to gain deeper insight. Users can connect to enterprise data directly, or they can import other data sets from from files or other data sources into Cognos Analytics. These data sources can be blended, cleansed and joined together to create a reusable **Data Module** for use in dashboards and reports, and or shared with other users in the organization. Although this lab has only one data source, we will still create a data module.

<img src="./cmedia/ca-image-15.png" >

1. **Select** the **New** menu from Navigation Bar on the left side

2. **Select** the **Data module** menu item.

<img src="./cmedia/ca-image-16.png" >

3. **Select** the **Data servers** menu from Navigation Bar on the left side

4. **Select** your **dashXXXXX Bank Customers** data server. You will see the schema you created earlier. 

<img src="./cmedia/ca-image-17.png" >

5. **Select** the **Schema** associated with your dashDB service username. For instance, mine is **DASH13919**.

6. **Select** the **Start** button.

### Data Modeling

Once a data source is selected, users can enter their desired search term(s) and click on Go to look for tables with data related to that search term. Cognos Analytics will analyze the data source and present table(s) that have some relation to the term you entered that you can add to your data module. Since we want to look into our Bank customers to analyze satisfaction and churn data,  

<img src="./cmedia/ca-image-18.png" >

1. In the intent panel, type **Customers**.

2. **Select** the **Go** button.

While we show multiple tables here, you should only see a single table, named **Bank Customers**.

3. **Select** the **Bank Customers** table.

4. **Select** the **Add this proposal** button.

<img src="./cmedia/ca-image-19.png" >

Your data module should look like the screen shot above.

5. **Select** the **Save** button on the top left corner of the toolbar (looks like a disk).

<img src="./cmedia/ca-image-20.png" >

6. **Select** the **My Content** folder.

7. **Enter** a module name of **Bank Customers Module**.

8. **Select** the **Save** button.

<img src="./cmedia/ca-image-21.png" >

9. **Expand** the **Bank Customers** table in the Data Module View to see all the columns.

<img src="./cmedia/ca-image-22.png" >

You have told us that your Data Scientists have found some interesting correlations between the number of late payments a customer has had in the past and their propensity to churn. Because this has been identified as an interesting factor for further analysis, we will divide the data into groups based on how many late payments they have had. 

10. **Select** the **ellipse** ... on the **Number of Late Payments** column to view the column menu items.

11. **Select** the **Create custom groups** menu item.

<img src="./cmedia/ca-image-23.png" >

We can see that Cognos Analytics suggests creating an equal distribution of the late payment values into 10 groups distributed evenly. However, we will create 3 groups based on the findings of the Data Scientists.

<img src="./cmedia/ca-image-24.png" >

1. **Change** the Group name to **Group Late Payments**.

2. **Change** the **How many groups?** number from **10 to 3**.

3. **Select** the **Custom** distribution radio button.

4. **Change** the lowest value to **1**

5. **Change** the middle value to **21**

6. **Change** the highest value to **3000**

7. **Select** the **Create** button.

<img src="./cmedia/ca-image-25.png" >

The data scientists have also observed a correlation between the number of credit applications a customer has submitted and their tendency to churn. So we will also create a another Custom group for the number of credit applications.

1. **Select** the **ellipse** ... on the **Number of Credit Applications** column to view the column menu items.
2. **Select** the **Create custom groups** menu item.

<img src="./cmedia/ca-image-26.png" >

1. **Change** the Group name to **Group Credit Applications**.

2. **Change** the **How many groups?** number from **10 to 3**.

3. **Select** the **Custom** distribution radio button.

4. **Change** the lowest value to **5**

5. **Change** the middle value to **26**

6. **Change** the highest value to **3000**

7. **Select** the **Create** button.

<img src="./cmedia/ca-image-27.png" >

8. **Select** the **Save** button on the toolbar to save the data module.

<img src="./cmedia/ca-image-28.png" >

9. **Go to** the top of the Cognos Analytics user interface and **Click** on the navigation drop down arrow.

10. **Select** the **- minus** sign next to the **Bank Customers Module** entry to close the module.

<img src="./cmedia/ca-image-29.png" >

11. **Select** the **My Content** menu from the left side main menu.

12. **Select** the **ellipse** ... in the right corner of the **Bank Customers Module**.

13. **Select** the **Open** menu item.

### Create Navigation Group

Navigation groups allow drill downs that align with how users want or need to analyze their business. In this case the Bankid column identifies whether the data is from "K Bank" or "N Bank". 

<img src="./cmedia/ca-image-30.png" >

1. **Select** the arrow next to the **Bank Customers** table to see the list of columns.

<img src="./cmedia/ca-image-31.png" >

2. **Scroll down** the list of columns to the **Bankid** column.

3. **Select** the **ellipse** ... on the **Bankid** column to view the column menu items.

4. **Select** the **Create navigation group** menu item.

In our Analysis we want to look at information by Originating Bank, churn, customer type, branch location and customer.

<img src="./cmedia/ca-image-32.png" >

5. **Rename** the Navigation Group to **Bank Churn**.

6. **Drag and Drop** the **Churn** column below Bankid.

7. **Drag and Drop** the **Customer Type** column below Churn.

8. **Drag and Drop** the **Home Branch State** column below Customer Type.

9. **Drag and Drop** the **Customer** column below Home Branch State.

10. **Select** the **Apply** button.

11. **Select** the **Save** button in the top left corner of the toolbar to save the data module.

## Step 2: Getting Insight

<img src="./cmedia/ca-image-33.png" >

1. **Go to** the top of the Cognos Analytics user interface and **Click** on the navigation drop down arrow.

2. **Select** the **Welcome** entry to go back to the Welcome page.

<img src="./cmedia/ca-image-34.png" >

3. **Go to** the bottom left portion of the Welcome page and **Select** the **+ New** menu.

4. **Select** the **Dashboard** menu item to create a new dashboard.

The Template window then appears, allowing you to select the type of dashboard and the template style. 

<img src="./cmedia/ca-image-35.png" >

5. **Select** the **Tabbed** template.

6. **Select** the **Tabbed layout** on the bottom row with 3 small panels on the top, and 2 full width panels below.

7. **Select** the **OK** button.

<img src="./cmedia/ca-image-36.png" >

Each panel on the template acts as a placeholder for dashboard objects, known as widgets. Templates are device aware and will auto-size to the screen of the device being used. As we build the dashboard, we will reference the location placement for widgets we create in the dashboard template using the panel numbers as designated and displayed above.

<img src="./cmedia/ca-image-37.png" >

8. **Select** the **+ plus sign** next to **Selected Sources** to choose a source.

9. **Select** the **My Content** folder.

10. **Select** the **Bank Customers Module** as the source.

11. **Select** the **Open** button.


### Designing a Dashboard

<img src="./cmedia/ca-image-38.png" >

Since this is the first dashboard we are creating you can see in the image above that the default name is Tab1.

1. **Click on** the **Tab 1** name. A menu will appear.

2. **Select** the **Edit** menu item that looks like a pencil.

<img src="./cmedia/ca-image-39.png" >

3. **Enter** a name of **Customer Satisfaction** and then click outside the name are to save the name.

<img src="./cmedia/ca-image-40.png" >

4. **Select** the triangle next to the **Bank Customers** table name to view the list of columns.

5. **Select** the **Satisfaction** column and **Drag and Drop** it into Panel 1.

> Remember the panel layout from above. Panel 1 is the panel in the top left corner of the template.

<img src="./cmedia/ca-image-41.png" >

6. **Resize** the **Satisfaction** number to span the entire panel by using the sizing controls.

Here we can see the average satifaction rating for our customers is 3.39 out of 5.

Next we want to look at satisfaction by customer type.

<img src="./cmedia/ca-image-42.png" >

1. **Select** the **Satisfaction** column

2. **Control-Click** on Windows or **Command-Click** on the Mac and **Select** the **Customer type** column

3. **Drag and Drop** the two columns to Panel 2 on the dashboard.

<img src="./cmedia/ca-image-43.png" >

4. **Resize** the **Customer Type-Satisfaction** graph to span across panel 1 and 2 by using the sizing controls.

Cognos Analytics gives a visualization to start based on the data types and number of values for the columns selected, but you can change these visualizations by selecting the **Change Visualization** icon. That will show the visualizations that best suit the data types of the columns inside the visualization. You can always select **More** if you do not see a format you like. You can click anywhere else in the dashboard to close this window.

5. **Select** the **Save** button on the toolbar to save the dashboard.

<img src="./cmedia/ca-image-44.png" >

6. **Select** the **My Content** folder.

7. **Enter** a dashboard name of **Bank Customer Analysis**.

8. **Select** the **Save** button.

> **Note -** If the data source panel is not open, from the Navigation panel on the left side of the screen, select sources to open the data source panel and select the **Bank Customers Module** we were working with.

<img src="./cmedia/ca-image-45.png" >

1. **Click on** the triangle next to **Navigation paths** to expand it.

2. **Click on** the triangle next to the **Bank Churn** navigation path to expand it.

3. **Click on** the triangle next to **Bank Customers** to expand it.

<img src="./cmedia/ca-image-46.png" >

4. From the **Bank Churn** navigation path, **Select** the Bankid column.

5. **Ctrl-Click or Command-Click** and **Select** the **Satisfaction** column under the **Bank Customers Module**

6. **Drag and Drop** these items to Panel 4 (the panel in the middle of the template).

<img src="./cmedia/ca-image-47.png" >

7. **Resize** the **Bankid-Satisfaction** graph to span the entire panel by using the sizing controls.

8. **Select** the **Save** button on the toolbar to save the dashboard.

> **Notice** that there is little difference in the overall satisfaction between the two banks.

<img src="./cmedia/ca-image-48.png" >

1. From the **Bank Customers** table **Select** the **Satisfaction** column.

2. From the **Bank Customers** table **Ctrl-Click or Command-Click** and **Select** the **Age Range** column.

3. From the **Bank Customers** table **Ctrl-Click or Command-Click** and **Select** the **Gender** column.

4. **Drag and Drop** these items to Panel 5 (the panel on the bottom of the template).

<img src="./cmedia/ca-image-49.png" >

5. **Resize** the **Bankid-Satisfaction** graph to span the entire panel by using the sizing controls.

6. **Select** the **Save** button on the toolbar to save the dashboard.

<img src="./cmedia/ca-image-50.png" >

7. **Click on** the **Bankid-Satisfaction** graph in Panel 5.

8. **Select** the **Visualization** icon.

<img src="./cmedia/ca-image-51.png" >

9. **Select** the **Heat Map** visualization from the panel of choices to change the graph to a Heat Map.

10. **Select** the **Arrow** to close the visualization menu.

11. **Select** the **Save** button on the toolbar to save the dashboard. 

<img src="./cmedia/ca-image-52.png" >

Your Dashboard should now like the screen shot above. **Notice** that on average Males are more satisfied than females, and that on the right, our older customers are the least satisfied.

Now, let's add another Tab to the Dashboard.  

<img src="./cmedia/ca-image-53.png" >

1. **Select** the **+ plus sign** next to the **Customer Satisfaction** tab to add a new tab.

<img src="./cmedia/ca-image-54.png" >

2. **Scroll down** and **Select** the 2 x 2 template with 4 rectangles in it.

3. **Select** the **USE** button.

<img src="./cmedia/ca-image-55.png" >

4. **Select** the **Tab 1** name area. A menu will appear.

5. **Select** the **Edit** icon that looks like a pencil.

<img src="./cmedia/ca-image-56.png" >

6. **Enter** a name of **Churn Analysis** and click outside the name area to save the name.

<img src="./cmedia/ca-image-57.png" >

> Note - This image depicts the numbering of the four panels to explain placement in the following steps.

As we said earlier, your data scientists have found that churn seems to be related to the number of credit applictions the customer has submitted, and the number of times they have had late payments. Remember we also created groups for late payments and credit applications, now let's create visualizations for these. 

<img src="./cmedia/ca-image-58.png" >

1. **Scroll** down to the bottom of the list of columns in the **Bank Customers** data module.

2. From the **Bank Customers** data module **Select** the **Group Late Payments**.

3. **Ctrl-Click or Command-Click** the **Count** column.

4. **Ctrl-Click or Command-Click** the **Churn** column.

5. **Drag and Drop** these columns onto Panel 1.

<img src="./cmedia/ca-image-59.png" >

6. **Resize** the graph you just created to span and use panel 1 and panel 2 by using the sizing controls.

7. **Select** inside the graph to get a menu of graph actions.

8. **Select** the **Visualization** menu item.

<img src="./cmedia/ca-image-60.png" >

9. **Select** the **Heat Map** visualization to change the graph to a Heat Map.

10. **Select** the **Arrow** in the top left of the visualization menu to close the visualization menu.

11. **Select** the **Save** button in the top left corner of the toolbar to save the dashboard.

> **Note** - Even though we created three groups we see four groups here. What is different?   
>   
> **Notice** that the group on the far right is blank. In this case there were some columns that had no value at all for the number of late payments. In this specific case does this mean that customer had no (ZERO) applications, or that someone forgot to fill in this field, or that there is an applicatio problem somewhere? We need to determine the source of the data and whether it is valid or needs to be fixed. We would need to verify this data with the bank data engineers.

Now you will add a visualization of churn to credit applications. 

<img src="./cmedia/ca-image-61.png" >

1. **Scroll** down to the bottom of the list of columns in the **Bank Customers** data module.

2. From the **Bank Customers** data module **Select** the **Group Credit Applications**.

3. **Ctrl-Click or Command-Click** the **Count** column.

4. **Ctrl-Click or Command-Click** the **Churn** column.

5. **Drag and Drop** these columns onto Panel 3.

<img src="./cmedia/ca-image-62.png" >

6. **Resize** the graph you just created to span and use panel 3 and panel 4 by using the sizing controls.

7. **Select** inside the graph to get a menu of graph actions.

8. **Select** the **Visualization** menu item.

<img src="./cmedia/ca-image-63.png" >

9. **Select** the **Heat Map** visualization to change the graph to a Heat Map.

10. **Select** the **Arrow** in the top left of the visualization menu to close the visualization menu.

11. **Select** the **Save** button in the top left corner of the toolbar to save the dashboard.

<img src="./cmedia/ca-image-64.png" >

> The Churn Analysis tab should look like the screen shot above. From these graphics we can see that our most loyal customers are the ones with the least credit applications and late payments.

> **Note -** We see the same thing in this graphic with some data being (blank). Again, we could assume that a blank is a zero, but for more accurate analysis we should clean up the data and update the blnk to a 0 (zero).

Let's go back to the Customer Satisfaction tab, since that was the main reason for the work we have done so far. 

<img src="./cmedia/ca-image-65.png" >

In the middle of the window there are two bars, **K** and **N** (K Bank and N Bank).

1. **Click** on the **Bankid** label between the bars.

2. **Select** the **drill down** button (second from the right).

<img src="./cmedia/ca-image-66.png" >

We now see two bars, yes and no, "yes" means the customer has left the bank and "no" means they have not left the bank. Let’s investigate the customers who have left the bank (yes). We can also see (in the Satisfaction graph in the top left corner) that the satisfaction scores are lower for the yes bar (the people who have left). 

<img src="./cmedia/ca-image-67.png" >

3. **Click** on the **yes** bar on the right.

4. **Select** the **drill down** button (second from the right).

<img src="./cmedia/ca-image-68.png" >

We notice that all of the visualizations change to be relative to customers who left, and that the satisfaction score changes to a lower number, which makes sense. We now see that our Small Business customers have the lowest satisfaction scores **3.04**. You can hover over any of the bars in the graph to get more details about the metric. Hover over the **Small Business** bar in the graph and you will see the **3.04** satisfaction score.

<img src="./cmedia/ca-image-69.png" >

We can dig deeper into these customers by drilling down further.

1. **Click** on the **Small Business** bar in the graph.

2. **Select** the **drill down** button (second from the right). 

<img src="./cmedia/ca-image-70.png" >

This shows the States of the customers who left the bank. In this case since we are filtered on Small Business, we see the satisfaction level of all Small Business customers who have left, by their state. 

To find the state with the lowest satisfaction score:

<img src="./cmedia/ca-image-71.png" >

1. **Click** on the **Satisfaction (Average)** axis title on the left hand side of the chart.

2. **Select** the **Sort** button.

<img src="./cmedia/ca-image-72.png" >

3. **Select** the **Sort descending** menu item.

<img src="./cmedia/ca-image-73.png" >

We see that Rhode Island has the lowest satisfaction level. We can drill down to find out which customer(s) from Rhode Island closed their accounts. 

<img src="./cmedia/ca-image-74.png" >

1. **Click** on the **Rhode Island** bar in the graph.

2. **Select** the **drill down** button (second from the right).

<img src="./cmedia/ca-image-75.png" >

We see that we had one customer (UX10401) leave us from Rhode Island, and their satisfaction level was 2.  

Additionally, if we look at the bar below, we can see that this customer was a 70 - 79 year old female.

> **Note -** You can click on any part of the dashboard and the rest of the dashboard will filter based on the value you select. Also, we would usually title these graphs, set maximums on graphs, specify different colors, etc. to make the Dashboard more appealing before sharing across the enterprise (or at the board meeting). But in the sake of time we will skip that for this demo.


# Take a screen capture or screen shot of this dashboard tab to show that you have completed the lab. 
