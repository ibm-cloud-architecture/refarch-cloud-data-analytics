## Step 1: Setup Cognos


[Click Here to Go to Cognos Analytics on Cloud](https://www.ibm.com/analytics/us/en/technology/products/cognos-analytics/)


<img src="./cmedia/ca-image-01.png" >

1. **Select** the **Sign In** button in the top right corner.

<img src="./cmedia/ca-image-02.png" >

2. **Enter** your IBM Account.

**Note -** Cognos Analytics on Cloud checks if the IBM account entered is associated with an IBM w3ID. If you are an IBM employee with a w3ID, complete the login process using section [Authenticate uisng your IBM w3ID](#w3). Otherwise, continue with step 3 and 4 below:

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
8. **Select** the **+ plus sign** right next to the drow down list box of signons.

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

5. **Select** the **Save** button on the top left corner of the toobar (looks like a disk).

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

> Remember the panel layout fro above. Panel 1 is the panel in the top lef corner of the template.

<img src="./cmedia/ca-image-41.png" >

6. **Resize** the **Satisfaction** number to span the entire panel by using the sizing controls.

Here we can see the average satifaction rating for our customers is 3.39 out of 5.

Next we want to look at satisfaction by customer type.

<img src="./cmedia/ca-image-42.png" >

1. **Select** the **Satisfaction** column
2. **Control-Click** on Windows or **Command-Click** on the Mac and **Select** the **Customer type** column
3. **Drag and Drop** the two columns to Panel 2 on the dashboard.

<img src="./cmedia/ca-image-43.png" >

4. **Rezie** the **Customer Type-Satisfaction** graph to span across panel 1 and 2 by using the sizing controls.

Cognos Analytics gives a visualization to start based on the data types and number of values of the columns selected, but you can change these visualizations by selecting the **Change Visualization** icon. That will show the visualizations that best suit the data types of the columns inside the visualization. You can always select **More** if you do not see a format you like. You can click anywhere else in the dashboard to close this window.

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

7. **Rezie** the **Bankid-Satisfaction** graph to span the entire panel by using the sizing controls.
8. **Select** the **Save** button on the toolbar to save the dashboard.

> **Notice** that there is little difference in the overall satisfaction between the two banks.

<img src="./cmedia/ca-image-48.png" >

1. From the **Bank Customers** table **Select** the **Satisfaction** column.
2. From the **Bank Customers** table **Ctrl-Click or Command-Click** and **Select** the **Age Range** column.
3. From the **Bank Customers** table **Ctrl-Click or Command-Click** and **Select** the **Gender** column.
4. **Drag and Drop** these items to Panel 5 (the panel on the bottom of the template).

<img src="./cmedia/ca-image-49.png" >

5. **Rezie** the **Bankid-Satisfaction** graph to span the entire panel by using the sizing controls.
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

1. **Select** the **+ plus sign** next to the ** Customer Satisfaction** tab to add a new tab.

<img src="./cmedia/ca-image-54.png" >

2. **Scroll down** and **Select** the 2 x 2 template with 4 rectangles in it.
3. **Select** the **USE** button.

<img src="./cmedia/ca-image-55.png" >

4. **Select** the **Tab 1** name area. A menu will appear.
5. **Select** the **Edit** icon that looks like a pencil.

<img src="./cmedia/ca-image-56.png" >

6. **Enter** a name of **Churn Analysis** and click outside the name area to save the name.

<img src="./cmedia/ca-image-57.png" >

> Note - The four panels are numbered in this image to explain placement in the following steps.

As we said earlier, your data scientists have found that churn seems to be related to the number of credit applictions the customer has submitted, and the number of times they have had late payments. Remember we also created groups for late payments and credit applications, now let's create visualizations for these. 

![](cmedia/image66.png)

Add a visualization of churn to late payments using the following steps. 

1. Under Bank Customers in the data module on the left select Group Late Payments

1. Under Bank Customers Ctrl-Click (Command-Click) the Count column 

1. Under Bank Customers Ctrl-Click (Command-Click) the Churn column

1. Drag these items to Panel 1

1. Click on a corner or side of the visualization to expand it to use both panel 1 and panel 2

1. Change the Visualization to a Heat map

> Note - 
> Even though we created three groups we see four groups here. What is different?   
>   
> Notice that the group on the far right is (blank). In this case there were some columns that had no value at all for the number of late payments. In this specific case does this mean that customer had no (ZERO) applications, or that someone forgot to fill in this field, or that there is an applicatio problem somewhere? We need to determine the source of the data and whether it is valid or needs to be fixed. We would need to verify this data with the bank data engineers.


![](cmedia/image67.png)

Now add a visualization of churn to credit applications using the following steps. 


1. Under Bank Customers select Group Credit Applications

1. Under Bank Customers Ctrl-Click (Command-Click) the Count column

1. Under Bank Customers Ctrl-Click (Command-Click) the Churn column 

1. Drag these items to Panel 3

1. Click on a corner or side of the visualization to expand it to use both panel 3 and panel 4

1. Change the Visualization to a Heat map

**From these graphics we can see that our most loyal customers are the ones with the least credit applications and late payments.**

> Note - 
> We see the same thing in this graphic with some data being (blank). Again, we could assume that a blank is a zero, but for more accurate analysis we should clean up the data and update the blnk to a 0 (zero).


**The Churn Analysis tab should look like this**

![](cmedia/image68.png)

Save the Dashboard
  

Let's go back to the Customer Satisfaction tab, since that was the main reason for the work we have done so far. 

![](ca2media/image005.png)

In the middle of the window we two bars, K and N (K Bank and N Bank).

Click the Bankid label under those bars and select drill down

![](ca2media/image006.png)

We now see two bars, yes and no (yes means the customer has left the back, no they have not). 

Let’s investigate the customers who have left (yes). 

We can see that the satisfaction scores are lower for the yes bar (the people who have left). Click on the y bar and click on drill down. We notice that all of the visualizations change to be relative to customers who left, and that the satisfaction score changes to a lower number, which makes sense. 

![](ca2media/CA0001.png)


We now see that our Small Business customers have the lowest satisfaction scores (3.04). We can dig deeper into these customers by clicking on the Small Business bar and click Drill down. 

![](ca2media/image007.png)


This shows the States of the customers who left the bank. In this case since we are filtered on Small Business, we see the satisfaction level of all Small Business customers who have left, by their state. To find the state with the lowest satisfaction score:

1. Click the Satisfaction (Average) axis title on the left hand side of the chart

1. Select the Sort icon

1. Select Sort desending

![](ca2media/image008.png)

We see that Rhode Island has the lowest satisfaction level. We can select the Rhode Island bar and select drill down to find out which customer(s) from Rhode Island closed their accounts. 

![](ca2media/CA0002.png)

We see that we had one customer (UX10401) leave us from Rhode Island, and their satisfaction level was 2.  

![](ca2media/CA0003.png)

Additionally, if we look at the bar below, we can see that this customer was a 70 - 79 year old female.

> Note -
>
>You can click on any part of the dashboard and the rest of the dashboard will filter based on the value you select.


**We would usually title these graphs, set maximums on graphs, specify different colors, etc. to make the Dashboard more appealing before sharing across the enterprise (or at the board meeting). And you can see in the images that we have done that here. But, for the purposes of this demo we will have you do that.**


# Take a screen capture or screen shot of this dashboard tab to show that you have completed the lab. 
