# Moving data and workloads from on-premises to the cloud for more agile analytics

## Table of Contents
- **[Introduction](#introduction)**
- **[Narrative](#narrative)**
- **[Solution Overview](#solution-overview)**
- **[Prerequisites](#prerequisites)**
- **[Project Components](#project-components)**
- **[Setup the reference solution in IBM Cloud](#Setup-the-reference-solution-in-ibm-cloud)**
    

PLACEHOLDERS  
- **[Step 2: Provision a Kubernetes cluster on IBM Bluemix Container service](#step-2-provision-a-kubernetes-cluster-on-ibm-bluemix-container-service)**
        - [Lite Cluster](#lite-cluster)
        - [Paid Cluster](#paid-cluster)
    - **[Step 3: Deploy reference implementation to Kubernetes Cluster](#step-3-deploy-reference-implementation-to-kubernetes-cluster)**
        - [Deploy Bluecompute Community Edition to Lite Cluster](#deploy-bluecompute-community-edition-to-lite-cluster)
            - [Delete Bluecompute Community Edition from Lite Cluster](#delete-bluecompute-community-edition-from-lite-cluster)
        - [Deploy Bluecompute Community Edition to Local Minikube Cluster](#deploy-bluecompute-community-edition-to-local-minikube-cluster)
            - [Delete Bluecompute Community Edition from Local Minikube Cluster](#delete-bluecompute-community-edition-from-local-minikube-cluster)
        - [Deploy Bluecompute to Paid Cluster](#deploy-bluecompute-to-paid-cluster)
            - [Delete Bluecompute from Paid Cluster](#delete-bluecompute-from-paid-cluster)

## Introduction

This project provides a reference implementation for moving data from on-premises relational database(s) into a Cloud Managed Database Service (dashDB) so that the data can be analyzed quickly, easily, and without the need to setup any new hardware or request resources from the IT department. In this example, the on premises databases are in two different RDBMS'es to emulate two different organizations. However, you could use a similar pattern and set of step to copy from a single database into the cloud as well.

In this case, one organization is using IBM's PureData System for Analytics (Netezza) and the other DB2 on Linux for their data warehouses. The data from these systems will be pushed into dashDB in the cloud so that it can be combined and analyzed as a single entity.  

**We will provide two mechanisms for moving the data from on-premises to the cloud, Bluemix Data Connect and Lift CLI, so that you can choose the method based on who you demoing to.** Data Connect is a cleaner, easier solution for one time moves, and best used when demoing to Business Users (LOB managers and executives). Lift CLI is how we would productionalize the initial and delta data load process, and best used when demoing to IT.

### Loading data using IBM Data Connect

![Overview](Images/SystemOverviewConnect2.png)

### Loading data using IBM Bluemix Lift CLI

![Overview](Images/SystemOverviewLift1.png)

## Narrative 

Consider the following scenario: You are talking to the Chief Marketing Officer (CMO) at "K Bank". 

Hi Ms. Smith, I know that "K Bank" just bought "N Bank", and I just came from a meeting on how you plan to integrate the two companies’ systems, and it is going to take quite a while. I would think that many people, and you in particular, can’t wait for a year or more for the integrated data to start reaching out to your customers.

I know that "K Bank" has been doing churn analytics for some time, but the team at "N Bank" has not. "K Bank" has found that customer loss (churn) is directly related to the customer's satisfaction level. This is kind of obvious, so it would be interesting to see how these churn prediction models could be used to looks at "N Bank" customers and identify who might be at risk of leaving. Since "K Bank" just spent a lot of money to acquire "N Bank", you do not want to lose any customers if you can help it.  

IBM can help you combine the data from both banks now, so that you can get access to this combined data within days, without putting any load on your IT staff who is already overloaded with the consolidation.  We can use IBM's fully managed cloud services to copy data from your current on-premises systems in each bank into a cloud data warehouse and give you a single view of your customers across both banks.
 
Once you have that data at your fingertips, you can explore the data and discover how satisfied your customers are, within each Bank and across both Banks. You can also identify which customers are leaving the bank and which ones you should strive to retain.

We can quickly show you how to create a dashboard to showcase your findings, use it to tell a story of what you discovered and the actions you might want to take base on this analysis.

## Solution Overview

The solution is a set of Business Inteligence (BI) tools that allow Business Users to get quick but important insights from the data. In order to gain this insight the data from both bank systems need to be moved from their data centers into a common repository. Because IT cannot support creating and managing a new system and moving the data, the new, common repository needs to be hosted as a managed cloud service. The BI tools will then be connected to this new repository and the existing analytical reports will be run. 

## Prerequisites

You will need the following:

 - A Bluemix account
 - VMware
      - VMware Player or VMware Workstation for Windows
      - VMware Fusion (Full or 30 day trial) for OSX
 - Download the [VMware Image](https://ibm.box.com/s/50uj4kfg87qe3rd3icjfvlx94xaygdmr) 
      - Note: The VMware image will consume 20GB of local disk and 3GB RAM. Users with limited RAM (8GB) will want to shut down as many applications as possible prior to launching VMware.
 - A provisioned Data Connect Starter service in Bluemix
 - A provisioned dashDB for Analytics (**Db2 Warehouse on Cloud** *as of ~July 18*) Entry service in Bluemix
 - dashDB access credentials
 - A [Cognos Anlaytics Trial](https://ca-trial.mybluemix.net/) 

> **Note**  
If you need help with the pre-requisites, go to the [Prereq Step by Step Directions](https://github.com/ibm-cloud-architecture/refarch-cloud-data-analytics/blob/master/PreWork.md)  


## Project Components

There are a few components of this solution. We used a VM to emulate the on premises systems, PureData System for Analytics (Netezza) and DB2. Both of these systems are commonly used by financial firms due to the performance and security they provide - not only for data at rest, but also data as it is being queried.   

We chose dashDB for Analytics (to be renamed **Db2 Warehouse on Cloud** as of ~July 18th) as the combined repository since it is a fully namaged service in the cloud that can be expanded easily, needs no administration, and has built in encryption and security. dashDB is ISO 27001, SOC 2, SOC 3 and HIPAA certified.

Data Connect uses the Secure Gateway to encrypt the data on the wire and Lift uses Aspera to transfer the data using very high levels of compression as well as automatic encryption.   

 - [BLAHBLAHBLAH](https://github.com/ibm-cloud-architecture/refarch-cloudnative-bluecompute-mobile/tree/kube-int) - XXXX
 


## STOP HERE FOR NOW...YOU WILL HAVE NO FINE WINE UNTIL IT IS TIME



## Setup the reference solution in IBM Cloud

To run the solution demo you will need to download and start the VM, configure your Bluemix environment, and run the data movement service. These configuration steps will deploy a framework for running Cognos Analytics.

### Start the Virtual Machine


## Step G: Launch the Data Connect Service

- Clone the base repository:  
    **`$ git clone https://github.com/ibm-cloud-architecture/refarch-cloudnative-kubernetes`**

- Clone the peer repositories:  
    **`$ cd refarch-cloudnative-kubernetes && sh clonePeers.sh`**

#### Install IBM Bluemix CLI and Container Service Plugin, Kubernetes CLI and Helm

To install and test BlueCompute stack in IBM Bluemix, you need the following tools:
- [Cloud Foundry CLI](https://github.com/cloudfoundry/cli/releases)
- [Bluemix CLI](http://clis.ng.bluemix.net/ui/home.html)
- [Bluemix Container Service plugin](https://console.ng.bluemix.net/docs/containers/container_cli_cfic.html)
- [Kubernetes cli](https://kubernetes.io/docs/tasks/kubectl/install/) (`kubectl`)
- [Helm](https://github.com/kubernetes/helm) (Helm is Kubernetes package manager)

We have developed a wrapper script to install all above tools on your Mac or Linux machine. In your root directory, execute the following command:

```
$ ./install_cli.sh
```
This script will install the CLIs for Bluemix, Container Service, Kubernetes, Helm, and jq for configuration parsing.
It will ignore what's already installed.

#### Create a New Space in Bluemix

1. Click on the Bluemix account in the top right corner of the web interface.
2. Click Create a new space.
3. Enter "cloudnative-dev" for the space name and complete the wizard.

#### Create a Bluemix API Key

1. Click on the Bluemix account in the top right corner of the web interface.
2. Click Create a new space.
3. Enter "cloudnative-dev" for the space name and complete the wizard.

```
$ bx login
$ bx iam api-key-create <api-key-name>
```

Please keep this API key as it WILL BE NEEDED in future steps.

### Step 2: Provision a Kubernetes cluster on IBM Bluemix Container service

Once you created Bluemix account and space, you will be able to provision/create a Kubernetes cluster with following instructions:

```
$ bx login
$ bx cs init
```

#### Lite Cluster

The Lite tier of Bluemix Container Service is free of charge and allows users to provision a cluster with one worker node of type `u1c.2x4` (2 core, 4GB memory, 100GB storage, 100Mbps network).  This should be sufficient to run the entire BlueCompute stack.

```
$ bx cs cluster-create --name <cluster-name>
```

#### Paid Cluster

The Paid tier of Bluemix Container Service allows users to provision a cluster in a user-selected datacenter, with configurable number of worker nodes and configurable number of worker node sizes.  The cluster is provisioned in the linked IBM Bluemix Infrastructure Account.  With a paid cluster, the Ingress Controller and Load Balancer are enabled.

First, retrieve the list of valid locations:

```
$ bx cs locations
```

Choose a location to discover the available worker node sizes:

```
$ bx cs machine-types <location>
```

(Optional) If you already have devices in Bluemix Infrastructure, you may select a specific public/private VLAN pair to place the worker nodes on.

```
$ bx cs vlans <location>
```

Make note of the `Router` of each VLAN; you must select a *private* and a *public* VLAN behind the same physical *router* in Bluemix Infrastructure.  These look like `fcr01a.dal10` for a public VLAN, and `bcr01a.dal10` for a private VLAN; ensure that the number in the router's name (e.g. `01`) matches for the public and private VLAN.

The final command looks like:

```
$ bx cs cluster-create \
    --name <cluster-name> \
    --location <location> \
    --machine-type <machine-type> \
    --private-vlan <private-vlan-id> \
    --public-vlan <public-vlan-id> \
    --workers <number-of-workers>
```

For example:

```
$ bx cs cluster-create \
    --name my-kube \
    --location dal10 \
    --machine-type b1c.16x64 \
    --private-vlan 1221455 \
    --public-vlan 1325142 \
    --workers 3
```

The entire process may take a few minutes, as the automation creates a master node in the IBM managed Bluemix Infrastructure account , then worker node(s) in your Bluemix Infrastructure account.  Monitor the cluster creation using:

```
$ bx cs clusters
$ bx cs cluster-get <cluster-name>
```

and the individual cluster node statuses:

```
$ bx cs workers <cluster-name>
```

### Step 3: Deploy reference implementation to Kubernetes Cluster

We packaged all the application components as Kubernetes [Charts](https://github.com/kubernetes/charts). To deploy the Bluecompute solution, please follow the instructions in the following sections.

#### Deploy BlueCompute Community Edition to Lite Cluster

We created a couple of handy scripts to deploy the Bluecompute Stack for you in the Lite Cluster. If you haven't done so, please [Create a New Bluemix Space](#create-a-new-space-in-bluemix) and [Create a Bluemix API Key](#create-a-bluemix-api-key). Then, run the following command:

```
# Supported Regions:
# ng
#  - (US South) - Default
# eu-de
#  - (Germany)

$ ./install_bluecompute_ce.sh <cluster-name> <bluemix-space-name> <bluemix-api-key> <Optional:region>
```

Once the actual install of Bluecompute takes place, it takes about 5-10 minutes to be fully deployed. So it might look like it's stuck, but it's not. Once you start to see output, look for the `Bluecompute was successfully installed!` text in green, which indicates that the deploy was successful and cleanup of jobs and installation pods will now take place. Please wait a minute or two to access the web app since some of the Microservices Pods are still initializing.

At the very end you will get a **URL** (i.e. http://169.48.138.137:31469) to access the Bluecompute Web App.    

![BlueCompute Detail](static/imgs/bluecompute_web_home.png?raw=true)  
You can reference [this link](https://github.com/ibm-cloud-architecture/refarch-cloudnative-bluecompute-web/tree/kube-int#validate-the-deployment) to validate the sample web application.  

Login Credentials: Once you are on the Bluecompute Web App, use the following test credentials to login:
- **Username:** user
- **Password:** passw0rd

That's it! **Bluecompute is now installed** in your Kubernetes Cluster. To see the Kubernetes dashboard, run the following command:

`$ kubectl proxy`

Then open a browser and paste the following URL to see the **Services** created by Bluecompute charts:

  http://127.0.0.1:8001/api/v1/proxy/namespaces/kube-system/services/kubernetes-dashboard/#/service?namespace=default

If you like to see **installation progress** as it occurs, open a browser window and paste the following URL to see the Installation Jobs. About 17 jobs will be created in sequence:

  http://127.0.0.1:8001/api/v1/proxy/namespaces/kube-system/services/kubernetes-dashboard/#/job?namespace=default

Be mindful that jobs come and go as new charts are getting installed.

**Notes:**

The *install_bluecompute_ce.sh* script will do the following:
1. Ask you login to Bluemix.
2. Initialize Container Plugin (bx cs init).
3. Unless already provided, it will create a Bluemix API Key
    * Not needed to deploy the reference application stack but will be needed for [DevOps and CI/CD](#devops-automation-resiliency-and-cloud-management-and-monitoring)
4. Get cluster configuration and set your terminal context to the cluster.
5. Initialize Helm.
6. Install the entire *Reference Application* Stack by installing the individual Helm charts. i.e.
    * `cd docs/charts`
    * `$ helm install chart_name --name release_name`
    * It will create all the necessary configurations before deploying any pods.
7. Cleanup Jobs and Pods used to deploy dependencies.

##### Delete Bluecompute Community Edition from Lite Cluster
To delete the Bluecompute Stack from your cluster, run the following script:

```
# Supported Regions:
# ng
#  - (US South) - Default
# eu-de
#  - (Germany)

$ ./delete_bluecompute_ce.sh <cluster-name> <bluemix-space-name> <bluemix-api-key> <Optional:region>
```

