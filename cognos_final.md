# Visualize Your Data

"K Bank" has found that customer loss (churn) is directly related to the customer's satisfaction level. This is kind of obvious, so it would be interesting to see how these churn prediction models could be used to looks at "N Bank" customers and identify who might be at risk of leaving. Since "K Bank" just spent a lot of money to acquire "N Bank", you do not want to lose any customers if you can help it.

Now that we have the data in one place, we can explore the data and discover how satisfied your customers are, within each Bank and across both Banks. You can also identify which customers are leaving the bank and which ones you should work to retain going forward. You can also create a dashboard to showcase your findings and use it to tell a story of what you discovered and any actions you might want to take base on this analysis for use in your next board meeting.

## Lets Get Started

Launch [Cognos Free Trial](https://www.ibm.com/analytics/us/en/technology/products/cognos-analytics/)
and SIGN IN to bring up the login page.

<img src="./cmedia/image2.png" >

The NEW User Experience brings you directly into the completely
redesigned Cognos Analytics User Interface (UI). All Cognos Analytics
Users begin their navigation here.

<img src="./cmedia/image3.png" >

## Create a Data server connection

![](/media/CA/ca1.png)

1. On the Welcome screen, select Manage on the bottom left side. Select Data server connections to create a new data server.

![](/media/CA/ca2.png)

1. Create a new data server connection by selecting the ‘+’ and Select dashDB as the type


![](/media/CA/ca3.png)

1. Rename the connection name from ‘New data server connection’ to ‘IA_Bank Customers’
1. Enter the your dashDB JDBC URL service credentials you obtained in the [prework exercise](https://github.com/ibm-cloud-architecture/refarch-cloud-data-analytics/blob/master/PreWork.md#step-d-create-the-dashdb-credentials).  Copy the "jdbcurl" (NOT the "ssljdbcurl") and paste into Cognos Analytics.  Your JDBC URL might look something like this (do not paste the quotes):  **"jdbc:db2://dashdb-entry-yp-dal09-08.services.dal.bluemix.net:50000/BLUDB"**

1. Create a signon associated to the new data connection. Select the ‘Use the following signon’ check box 
1. Select the  ‘+’ icon.

![](/media/CA/ca5.png)

1. Enter the your dashDB User ID
1. Enter your password and confirm your password
1. Test your new connection.  If it tests successfully, then
1. Save

If the test fails, check the userID, password, etc. and re-test.


Now we need to select the database schema (table owner) that we will use in this exercise. 

1. Select the Schema tab for the IA\_Bank Customers data server connection
1. Select the schema associated to your userid and select
1. Select Load metadata. 

![](cmedia/image25.jpg)

 When the schema is successfully loaded, the status button next to the schema will turn green

![](cmedia/image26.jpg)


## Create a Data Module

With Cognos Analytics, users are not restricted to only using existing enterprise data sources. Users can blend perosnal data or external data with enterprise data to gain deeper insight. Users can connect to enterprise data directly, or they can import other data sets from from files or other data sources into Cognos Analytics. These data sources can be blended, cleansed and joined together to create a reusable **data module** for use in dashboards and reports, and/or shared with other users in the organization. Although this lab has only one data source, we will still create a data module.

To create a new data module, select New from Navigation Bar on the left side of the Cognos Analytics screen and then select Data module

![](cmedia/image27.png)

This will take you to the Create data module screen and provide a list of options you can choose from. 

1. Select Data servers (because we are going to connect to the ‘IA_Bank Customers’ data server connection you created earlier.
1. Select IA_Bank Customers from the list. This will display the schema we created earlier. 
1. Select the ‘Schema’ associated with your dashDB instance, ours is **DASH106554** in this instance.

![](cmedia/image28.png)


Your schema will now be added to Selected sources list. Again ours is **DASH106554**.

Click on the Start button.

![](cmedia/image29.png)


## Data modeling

Once a data source is selected, Users can enter their desired search term and click on Go to look for tables with data related to that search term. Cognos Analytics will analyze the data source and present table(s) that have some relation to the term you entered that you can add to your data module. 

1. In the intent panel, type Customers since the user is interested in Customer information to
analyze Satisfaction and Churn information.
1. Click on Go
1. You should only see one table **Bank Customers**.  Select Bank Customers
1. Click on Add this proposal

![](cmedia/image30.png)

**Adding and Removing Tables from a Data Module**

If the proposed data module has a table the User decides is not needed,
it may be easily removed by right clicking on the table in the diagram
and selecting remove. **Right click on the 'Nbank Customers Old'** table
in the diagram and **select Remove**.

![](cmedia/image33.png)

Tables may also be deleted from the data module table list. Click on
'Old Key Niagra Customers' Brand in the data module panel.

**Right Click on 'Old Key Niagra Customers'** table in the list to open
the Options. **Select Remove**.

![](cmedia/image34.png)


For our analysis, the only table we need is ‘Bank Customers’, **Remove**
the following tables from the model

**Kbank Customers**

**Nbank Customers**

**Old Banking Customer Data**

Your model should look like this now

![](cmedia/image35.png)


We will save our data module now.

> Click Save.
>
> Select My Content.
>
> Type ‘Bank Customers Module’ for the name.
>
> Click Save

![](cmedia/image36.png)

Expand the Bank Customers table in the Data Module View

![](cmedia/image37.png)


Create Custom Groups
--------------------

You can see the columns in the table now and from the icons quickly
identify the numeric and non-numeric fields. **Select ‘Number of Late
Payments** **more option** and you can see for each column the actions
we can perform to improve the usability for users using this data
module. As you can see we can Create Calculations, Clean, Filter,
Rename, Hide, Remove or modify the properties for the item selected.
Here we are going to create a custom group. Select **Create custom
groups.**

![](cmedia/image38.png)


Our Data Scientists, using SPSS and Watson Analytics have found some
interesting probabilities related to customer churn based on the number
of late payments a customer has. We will create distribution groups to
reflect these finding so we can share this information with others. To
start we can see that the product has created an equal distribution of
the late payment values into 10 groups distributed evenly.

![](cmedia/image39.png)


We will create 3 groups based on their findings.

> Rename the Grouping to ‘Group Late Payments’
>
> Change the \# of groups from 10 to 3
>
> Select Custom
>
> Change the lowest value to 1
>
> Change the 2^nd^ value to 21
>
> Change the last value to 3000
>
> Select Create

![](cmedia/image40.png)


The data scientists have also observed some consistencies with the \# of
Credit Applications a customer makes to their tendency to Churn. We will
create another Custom group for Number of Credit Applications. Create a
new custom grouping for Number of Credit Applications.

We will create 3 groups based on their findings.

> Rename the Grouping to ‘Group Late Payments’
>
> Change the \# of groups from 10 to 3
>
> Select Custom
>
> Change the lowest value to 05
>
> Change the 2^nd^ value to 26
>
> Change the last value to 3000
>
> Select Create

![](cmedia/image41.png)


Save the data module

Create Navigation Group
-----------------------

A navigation group is a collection of non-measure columns that business
users associate for data exploration. Navigation groups can now be
defined as part of a data module to help users easily explore and drill
down to see their underlying data. These can be logical navigation paths
that follow a defined hierarchy, or they can be defined to allow users
to navigate and drill down in any order that makes sense for their
analysis.

We will start by **selecting the more option** for the field ‘Bankid’.
Bankid is at the bottom of the field list for the Bank Customers table,
just above the new Group calculation we just created. Another option to
locate the field is to type’Bank’ in the **Find** area of the data
module window. Select ‘Create navigation Group’

![](cmedia/image42.png)

In traditional BI and OLAP technologies, a drill down action required a
pre-defined hierarchical data structure so that you could drill down
from Year to Month, but was not defined to allow a User to drill from
Year to Product. Navigation groups are much more flexible and can
accommodate drill down that aligns with how users need to analyze their
business.

![](cmedia/image43.png)


In our Analysis we wish look at information by Bank, Churn, Customer
Type, Location and Customer.

> **Rename the Navigation Group to Bank Churn Drill Path**
>
> **Drag Churn below Bankid**
>
> **Drag Customer Type below Churn**
>
> **Drag Home Brnch State below Customer Type**
>
> **Drag Customer below Home Branch State**
>
> **Click Apply**

![](cmedia/image44.png)


**Save the Data Module**

There are many more things to do in this data module, but for timing we
will save it and start finding insights.

Create Dashboard for Insights
=============================

We will now create a dashboard to analize the information created in our
data module.

Create a new dashboard from the Navigation pane

![](cmedia/image45.png)


Working with Templates
----------------------

The Template window appears allowing the user to select the type of
dashboard and the template style. Select the tabbed dashboard style.
This will allow you to have multiple pages for your dashboards. Select
the template with the three (3) small panels across the top, and two (2)
panels below. Click OK

![](cmedia/image46.png)


Each panel on the template acts as a placeholder for dashboard objects,
known as widgets. Templates are device aware and will auto-size to the
screen of the device being used.

Cognos Analytics provides many “out of the box” templates to choose
from. This library of templates is based on dashboard design best
practices. The templates are simply guidelines that allow quick and
visually appealing layout of widgets onto the dashboard. However, users
may still customize layouts to suit their preferences and may also
choose to start from a freeform (blank) template.

As we build the dashboard, we will reference the location placement for
widgets in the dashboard template using the following panel numbers

![](cmedia/image47.png)


As we start our dashboard design we will be asked to select the data
sources to use. We will select the data module we just created.
Dashboards support the use of many data sources, in this example we will
only use 1

> Select the '+' to add sources to the Dashboard
>
> Select My Content
>
> Select Bank Customers Module
>
> Click Open

![](cmedia/image48.png)


Working with Dashboard Design
-----------------------------

Rename Tab1. To rename the dashboard tab, click on the tab name “Tab 1”
to bring up the On-Demand Toolbar. Select the Pencil and rename the tab
to 'Customer Satisfaction'

![](cmedia/image49.png)


Expand Bank Customers and drag Staisfaction to Panel 1. Here we can see
the average Satifaction rating by our customers is 3.39.

Satisfaction is very easy to locate here because its one of the first 10
fields in the list, again like everything else in Cognos Analytics there
is a Find area where you can find fields very quickly.

![](cmedia/image50.png)

Next we will select Satisfaction and Ctrl Click Customer type and drag
it to Panel 2. Cognos Analytics gives me a visualization to start based
on the items selected. I can change these visualizations by selecting
the Change Visualization icon.

![](cmedia/image51.png)


By Deault we will show the visualizations that best suit the items and
there types inside the visualization. You can always select ‘**More**’.
Click anywhere else in the dashboard to remove this window.

![](cmedia/image52.png)


Select the bar chart just created, we will now look at actions available
to you from the menu bar.

> The View widget icon allows users to decide which widgets will be
> connected to which other widgets in the dashboard. By default all
> widgets in the dashboard are automatically connected without any
> coding.
>
> The pin will pin the widget for further use in other dashboards or to
> be used for story telling.
>
> The properties item is what we will look at now. The properties allows
> you to customize and change the properties of the widget
>
> The user icon we talked about earlier as well as the help.

![](cmedia/image53.png)

Select the Properties Icon for the bar chart. Under the General Area, we
can change the color pallette, column color, maintain axis scale, and
Hide axis titles. Also, if dealing with changing data, set the refresh
rate for this widget to pickup the refreshed data in near real time
without having to take a user action. If refresh data set is on, we
first verify the data is changed before resubmitting the query of the
widget.

Here I have set the Column Color to Green and I have enabled ‘Hide axis
titles’

![](cmedia/image54.png)


Under the General Tab you see options to set the ‘Fill color’, ‘Border
color’ and you can set the Opacity of the widget of object selected in
the dashboard. If we had a image selected here, we might change the
Opacity to a lower number to use it as a background image for the Tab
and/or individual widget.

![](cmedia/image55.png)


To remove the Properties, click the Properties icon on the menu bar
again.

Note : The properties will change depending on the type of visualization
or object selected. For instance if a text object is selected, you would
see properties associated with a text item. The same is true if a
picture or video object is selected.

Resize the Customer Type Satisfaction bar chart to span Panel 2 and 3 by
dragging the resize button on the right to the end of the template to
look like this.

![](cmedia/image56.png)


Let’s save the Dashoard

> Click Save
>
> Select My Content
>
> Name the Dashboard ‘Bank Customer Analysis
>
> Click Save

![](cmedia/image57.png)

If the data source panel is not open, from the Navigation panel, select
Sources to open the data source panel. The Data Source panel displays
the Banking Customers Source we are working with.

![](cmedia/image58.png)

Expand ‘Navigation paths’ and ‘Bank Customers’ to list the items.

> From Navigation Paths under Bank Churn Drill Path select Bankid
>
> Ctrl-Click Satisfaction under Bank Customers
>
> Drag these items to Panel 4

![](cmedia/image59.png)

For Panel 5

> Under Bank Customers Select Satisfaction
>
> Under Bank Customers Age Range
>
> Under Bank Customers Gender
>
> Drag these items to Panel 5

![](cmedia/image60.png)

Change the Visualization in Panel 5 to a Heat Map

![](cmedia/image61.png)

![](cmedia/image62.png)


Your Dashboard should like this now.

![](cmedia/image63.png)


Save the Dashboard

Create a New Tab in the Dashboard

![](cmedia/image64.png)


For the template we will choose the 2 x 2 Template and select USE

The 4 Panels are also numbered in this image

![](cmedia/image65.png)


Rename the tab ‘Churn Analysis’

Make Panel 1 and 2 look like this using these steps

> Under Bank Customers Select Group Late Payments
>
> Under Bank Customers Ctrl-Click Count
>
> Under Bank Customers Ctrl-Click Churn
>
> Drag items to Panel 1
>
> Expand Visualization to use Panel 1 and 2
>
> Change the Visualization to a Heat Map

![](cmedia/image66.png)


Make Panel 3 and 4 look like this using these steps

> Under Bank Customers Select Group Credit Applications
>
> Under Bank Customers Ctrl-Click Count
>
> Under Bank Customers Ctrl-Click Churn
>
> Drag items to Panel 3
>
> Expand Visualization to use Panel 3 and 4
>
> Change the Visualization to a Heat Map

![](cmedia/image67.png)


The Churn Analysis Tab Should now look like this

![](cmedia/image68.png)


Save the Dashboard

Using Properties for each object, make this Dashboard visually appealing
by moving legends and adding titles and removing titles.

Find Insights in the Information
================================

Explore the information in the Dashboard and Share 3 Insights from the
Information you created

Insight 1
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

Insight 2
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

Insight 3
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_
