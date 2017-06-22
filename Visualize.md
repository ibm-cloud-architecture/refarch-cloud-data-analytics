## Visualize Your Data

After this workshop you will have a sense of the way in which IBM Cognos Analytics empowers business users to perform data discovery and to create dashboards and stories, enabling the creation and sharing of professional, enterprise ready reports.

I know that "K Bank" has been doing churn analytics for some time, but the team at "N Bank" has not. "K Bank" has found that customer loss (churn) is directly related to the customer's satisfaction level. This is kind of obvious, so it would be interesting to see how these churn prediction models could be used to looks at "N Bank" customers and identify who might be at risk of leaving. Since "K Bank" just spent a lot of money to acquire "N Bank", you do not want to lose any customers if you can help it.

IBM can help you combine the data from both banks now, so that you can get access to this combined data within days, without putting any load on your IT staff who is already overloaded with the consolidation. We can use IBM's fully managed cloud services to copy data from your current on-premises systems in each bank into a cloud data warehouse and give you a single view of your customers across both banks.

Once you have that data at your fingertips, you can explore the data and discover how satisfied your customers are, within each Bank and across both Banks. You can also identify which customers are leaving the bank and which ones you should work to retain going forward.

We can quickly show you how to create a dashboard to showcase your findings and use it to tell a story of what you discovered and any actions you might want to take base on this analysis.


   - **[PREWORK: Environment Setup](#prework-environment-setup)**
      - [Overview](#overview)  
      - [Step A: Download the lab files](#step-a-download-the-lab-files)  
      - [Step B: Create a Bluemix account](#step-b-create-a-bluemix-account)
      - [Step C: Create the Cloud Data Analytics lab services](#step-c-create-the-cloud-data-analytics-lab-services)
      - [Step D: Create the dashDB Credentials](#step-d-create-the-dashdb-credentials)
      - [Step E: Create a Cognos Analytics account](#step-e-create-a-cognos-analytics-account)
      - [Step F: Create a Watson Analytics account](#step-f-create-a-watson-analytics-account) 
      - [Step G: Create a GitHub account](#step-g-create-a-github-account)


## Environment Setup   

The Cloud Data Analytics lab is conducted using many components on the IBM cloud. It utilizes dashDB for Analytics to be renamed **Db2 Warehouse on Cloud** as of ~July 18th to persist data and Data Connect (and Lift CLI) to ingest data. These services are available and deployed from Bluemix, IBM’s cloud platform. This lab also leverages Cognos Analytics, IBM’s smart data reporting, analytics and visualization service on the cloud.

