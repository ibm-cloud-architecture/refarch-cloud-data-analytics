## Prerequisite Step By Step Directions

> **Note - If you already have any of the services, skip that step below**

   - **[PREWORK: Environment Setup](#prework-environment-setup)**
      - [Overview](#overview)  
      - [Step A: Download the lab files](#step-a-download-the-lab-files)  
      - [Step B: Create a Bluemix account](#step-b-create-a-bluemix-account)
      - [Step C: Create the Cloud Data Analytics lab services](#step-c-create-the-cloud-data-analytics-lab-services)
      - [Step D: Create the dashDB Credentials](#step-d-create-the-dashdb-credentials)
      - [Step E: Create a Cognos Analytics account](#step-e-create-a-cognos-analytics-account)
      - [Step F: Create a GitHub account](#step-f-create-a-github-account)

## Environment Setup   

The Cloud Data Analytics lab is conducted using many components on the IBM cloud. It utilizes dashDB for Analytics to be renamed **Db2 Warehouse on Cloud** as of ~July 18th to persist data and Data Connect (and Lift CLI) to ingest data. These services are available and deployed from Bluemix, IBM’s cloud platform. This lab also leverages Cognos Analytics, IBM’s smart data reporting, analytics and visualization service on the cloud.

This lab uses a Virtual Machine. You will need to have VMware Workstation or VMware Workstation Player on Windows or Vmware Fusion Pro on Mac/OSX. If you do not already have this, download the appropriate tool from 

   [Windows](https://www.vmware.com/products/player/playerpro-evaluation.html)

   [Mac OSX](https://www.vmware.com/products/fusion/fusion-evaluation.html)
   
   Download the lab [VMware Image](https://ibm.box.com/s/50uj4kfg87qe3rd3icjfvlx94xaygdmr) 
   
   Download the VMware image to your hard drive or an external USB drive. 
   **NOTE: The faster the drive, the better the performance will be.**

## Overview

On the following pages are a series of steps you need to complete before you do any of the labs. Each step outlines an easy to follow set of instructions that walks you through preparing your IBM cloud environment so you can do any of the labs you choose. It is a serial process so it’s important that you follow each step in sequence and do not deviate from the workflow or skip any steps in the process.

Step | Description
------------ | -------------
A | Download the lab files
B | Create a Bluemix account
C | Create the Cloud-Data-Analytics lab services
E | Create a Cognos Analytics account
F | Create a GitHub account

## Step A: Download the lab files

   **Download** the Customer data CSV files to your workstation. These files are used if you do not want to (or cannot) use the VM image to emulate the on-premises databases. Be sure to use the default names and the .csv file extention.
    
   Right click on this link and select Save Link As... [K Bank's data](https://github.com/ibm-cloud-architecture/refarch-cloud-data-analytics/raw/master/kbank_customers.csv)
    
   Right click on this link and select Save Link As... [N Bank's data](https://github.com/ibm-cloud-architecture/refarch-cloud-data-analytics/raw/master/nbank_customers.csv)
   
   <img src="./media/DL_1.png"/>     
  
   Make sure you do not change the name of the file, and that the comma-separated values Format is selected. 
   Click on Save.
   
   <img src="./media/DL_2.png"/> 


## Step B: Create a Bluemix account

You will need a Bluemix account. Follow the instructions in one of the sections below depending on whether or not you have a Bluemix account.

## If you have a Bluemix account...

### Log Into Bluemix 

### [Click Here to Login to Bluemix](https://console.ng.bluemix.net/)

> **Note** - The URL for Bluemix is https://console.ng.bluemix.net

<img src="./media/Step2-image-01.png">

1. **Select** the "Log In" button. When prompted, enter your Bluemix ID and password.

### Create a Bluemix space

<img src="./media/Step2-image-02.png">  

1. **Select** the account information area in the top right corner of your Bluemix home page.
2. **Select** the "Create a Space" link next to “Manage Organizations” below the space drop down list box.

  <img src="./media/Step2-image-03.png"/>

3. **Enter** “Cloud-Data-Analytics” (without quotes) for the space name.  
4. **Select** the “Create” button.  

> The space will be created and you will be brought into it. You should now see, in the top right corner, that you are in the “Cloud-Data-Analytics” space in your Bluemix organization. You will use this space to house the Cloud-Data-Analytics lab services. 

**Proceed to Step C: Create the Cloud Data Analytics Lab Services**

## If you don't have a Bluemix account...

### [Click Here to Register for a Bluemix Account](https://console.ng.bluemix.net/registration/)

<img src="./media/Step2-image-04.png"/>

**Enter** the required information *(required fields are marked with an asterick)* on the right side panel.

<img src="./media/Step2-image-05.png"/>

1. **Select** the "I'm not a bot" check box.

<img src="./media/Step2-image-06.png"/>

> **Note** - You may be asked to verify multiple images. Select the Skip or Next button as instructed until you get to a screen (as shown above) with a Verify button.

2. **Select** the images you are instructed to select. For instance, Select all squares with street signs. 
3. **Select** the "Verify" button.

<img src="./media/Step2-image-07.png"/>

4. **Review** and check or uncheck the options to be kept informed of products, services and offerings from IBM.
5. **Select** the "Create Account" button when it is enabled for selection.

<img src="./media/Step2-image-08.png"/>

A page will appear notifying you to check your email to complete your registraion. Check the inbox of the email address that you supplied to register for your Bluemix account and open the email.

<img src="./media/Step2-image-09.png"/>

6. **Select** the “Confirm your account” link.

<img src="./media/Step2-image-10.png"/>

You will be brought to a web page confirming that you sucessfully signed up for Bluemix and that it is now activated.

7. **Click** on the "Log in" link to log into your Bluemix account.

<img src="./media/Step2-image-11.png"/>

8. **Select** the checkbox to agree to the terms and conditions.
9. **Select** the “Continue” button.

> **Note** - I have redacted my email address on some screen shots to protect my identity, yours will be visible.

<img src="./media/Step2-image-12.png"/>

10. **Click** on the email address suggestion for an organization name. It will be automatically filled in for you as your organization name.
11. **Select** the “Create” button.

<img src="./media/Step2-image-13.png"/>

12. **Enter** “Cloud-Data-Analytics" (without quotes) as your Bluemix space name.
13. **Select** the "Create" button.

<img src="./media/Step2-image-14.png"/>

14. **Select** the "I'm Ready" button.

## Step C: Create the Cloud Data Analytics Lab Services

<img src="./media/Step3-image-01.png" />

1. **Select** the "Catalog" menu at the top of the Bluemix home page.

<img src="./media/Step3-image-02.png" />

2. **Enter** "data connect" (without quotes) in the catalog search area.  
3. **Click on** the “Data Connect” service.  

<img src="./media/Step3-image-03.png" />

4. **Enter** "CDA Data Connect” (without quotes) for the Service name.  (Use CDA as the acronym for Cloud-Data-Analytics).
5. **Enter** “CDA Data Connect” (without quotes) for the Credential name.  
6. **Select** the the "Create" button. The service will be created and the launch page is displayed.

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

<img src="./media/Step3-image-08.png" />

2. **Enter** "dashdb" (without quotes) in the catalog search area.  
3. **Click on** the “dashDB for Analytics” service.  

<img src="./media/Step3-image-09.png" />

4. **Enter** "CDA dashDB” (without quotes) for the Service name.   
5. **Select** the the "Create" button. The service will be created and the launch page is displayed.

<img src="./media/Step3-image-10.png" />

6. **Click On** the "CDA dashDB" service you just created from the list of services.

<img src="./media/Step3-image-10-1.png" 


## Step D: Create the dashDB Credentials

7. **Select** the "Service credentials” section of the "CDA dashDB" service launch page.   
8. **Select** the the "New credential +" button.

<img src="./media/Step3-image-11.png" />

9. **Enter** "CDA dashDB” (without quotes) for the credential name.   
10. **Select** the the "Add" button. The service credential will be created.

<img src="./media/Step3-image-12.png" />

11. **Select** the "View credentials v" down arrow to view the newly created credentials.

> **Note** - These are the "CDA dashDB" service credentials you will need to access the dashDB service in the Data Engineering and Data Science labs. Remember how to get back to this area of the service to access the credentials. I have redacted my password, to protect my identity, yours will be visible.

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


## Step E: Create a Cognos Analytics account

You will need a Cognos Analytics account. If you **don't** have an account:

[Click Here to Register for a Cognos Analytics account](https://www.ibm.com/analytics/us/en/technology/products/cognos-analytics/)

<img src="./media/CA1.png" />

1. **Select** the “Free Trial” button.

> Cognos Analytics is IBM account aware, but not Bluemix aware. 

If you have an IBM ID select login, otherwise enter your email and name, and set a password.

<img src="./media/CA2.png"/>

You will then see this screen, click on Continue

<img src="./media/CA3.png"/>

You now have a Cognos Analytics Account, and will see a screen like

<img src="./media/CA4.png"/>


## Step F: Create a GitHub account

You will need a GitHub account. If you **don't** have an account:

### [Click Here to Register for a GitHub account](https://github.com/)

<img src="./media/Step6-image-01.png" />

1. **Enter** a Username.
2. **Enter** an Email. I recommend using the same Email Address you used for your Bluemix account.
3. **Enter** a Password. Again, I recommend using the same password you used for your Bluemix account.
4. **Select** the "Sign up for GitHub" button.

<img src="./media/Step6-image-02.png"/>

5. **Choose** the "Unlimited repositories for free" plan (It should be selected by default).
6. **Select** the "Continue" button.

<img src="./media/Step6-image-03.png"/>

7. **Review** the "Tailor your experience" choices. Optionally select those you wish to supply or none of them.
8. **Select** the "Submit" button.

<img src="./media/Step6-image-04.png"/>

9. **Select** the "Start a project" button.

<img src="./media/Step6-image-05.png"/>

10. **Go to** the Email account you supplied during signup. Open the verification email sent to you by GitHub.

<img src="./media/Step6-image-06.png"/>

11. **Click On** the "Verify email address" link.

<img src="./media/Step6-image-07.png"/>

> You will be brought to a web page notifying you that your email was verified. 

12. **Select** the "X" in the top right corner to close the verification message.


> You have completed the pre-requisite steps. You can now begin completing the lab/demo.
