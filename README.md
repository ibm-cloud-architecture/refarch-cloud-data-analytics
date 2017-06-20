# Moving data and workloads from on premises to the cloud for more agile analytics

## Table of Contents
- **[Introduction](#introduction)**
- **[Narrative](#narrative)**
- **[System Overview](#system-overview)**
- **[Project Components](#project-components)**
- **[Run the reference application in IBM Cloud](#run-the-reference-application-in-ibm-cloud)**
    - **[Step 1: Environment Setup](#step-1-environment-setup)**
        - [Prerequisites](#prerequisites)
        - [Install IBM Bluemix CLI and Container Service Plugin, Kubernetes CLI and Helm](#install-ibm-bluemix-cli-and-container-service-plugin-kubernetes-cli-and-helm)
        - [Create a New Space in Bluemix](#create-a-new-space-in-bluemix)
        - [Create a Bluemix API Key](#create-a-bluemix-api-key)
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
- **[DevOps automation, Resiliency and Cloud Management and Monitoring](#devops-automation-resiliency-and-cloud-management-and-monitoring)**


## Introduction

This project provides a reference implementation for moving data from on premises relational databases running in two different organizations into a Cloud Managed Database Service (dashDB) so that the data can be analyzed quickly, easily, and without the need to setup any new hardware or request resources from the IT department.   

In this case, one organization is using our PureData System for Analytics (Netezza) and the other DB2 for their datawarehouses. The data from these systems will be pshed or pulled into dashDB in the cloud so that it can be combined and analyzed as a single entity.  

We will provide two mechanisms for moving the data from on premises to the cloud, Bluemix Data Connect and Lift CLI, so that you can choose the method based on who you demoing to. Data Connect is a cleaner, easier solution for one time moves, and best used when demoing to LOB managers and executives. Lift CLI is how we would productionalize this process if we were doing this over and over to keep the data in synch, and best used when demoing to IT.

## Loading data using IBM Bluemix Lift CLI

![Overview](SystemOverview2.png)
## Loading data using IBM Data Connect

![Overview](SystemOverview.png)

## Narrative 

Consider the following scenario. You are talking to the CMO at K Bank. 

Hi Ms. Smith, I know that K Bank just bought N Bank, and I just came from a meeting on how you plan to integrate the two companies’ systems, and it is going to take a while. I would think that many people, and you in particular, can’t wait for a year or more for the integrated data to start reaching out to your customers.

I know that K Bank has been doing churn analytics for some time, but the team at N Bank has not. It would be interesting to see how your models could be used to identify N Bank customers at risk of leaving a well. 

IBM can help you combine this data now so that you can get access to this combined data within days, without putting any load on your IT staff who is already over loaded with the consolidation.  We can use our fully managed cloud services to copy data from your current on-premises systems in each bank into a data warehouse and match customer names automatically to give you a single view of your customers across both banks.
 
Once you have that data at your fingertips, you can start asking even more probing questions, like –

Why are customers at risk of leaving? Which customers would be a loss and which would not? 

This will help you identify your most important customers, so you can work to keep them as long term customers. 

What do you think?

## Solution Overview

The solution is a set of Business Inteligence (BI) tools that allow the CMO or LOB manager to get quick, but important, insght from the data. In order to gain this insight the data from the two bank systems need to be moved from their data centers into a common repository. Because IT cannot support creating a new system and moving the data, that new/common repsoitry needs to be hosted in the cloud. The BI tools will then be connected to this new repository and the existing analytical reports will be run. 

## Project Components

There are a few components of this solution.  

- The Virtual Machine (VM) that contains the on premises databases. Due to license restricions this is only available to IBMers and Business Partners. The VM can be downloaded from (XXX)

- So that anyone can use the data and run the lab/demo we have also included the raw data (CSV) files from the two banks. You can download this to your computer and load them into dashDB using the steps provided. 
    [N Bank's data] (https://github.com/ibm-cloud-architecture/refarch-cloud-data-analytics/blob/master/N%20Bank%20Customer%20List%202017-06-19.csv)
    [K Bank's data] (https://github.com/ibm-cloud-architecture/refarch-cloud-data-analytics/blob/master/K%20Bank%20Customer%20List%202017-06-19.csv)
    
    

 - [refarch-cloud-data-analytics-VM](https://github.com/ibm-cloud-architecture/refarch-cloudnative-kubernetes/tree/kube-int)                    - The VM image of the on premises data repositories
 - [refarch-cloud-data-analytics-data](https://github.com/ibm-cloud-architecture/refarch-cloudnative-bluecompute-mobile/tree/kube-int) - The raw data that is preloaded in the databases in the VM
 

This project contains tutorials for setting up CI/CD pipeline for the scenarios. The tutorial is shown below.  
 - [refarch-cloudnative-devops-kubernetes](https://github.com/ibm-cloud-architecture/refarch-cloudnative-devops-kubernetes)             - The DevOps assets are managed here

This project contains tutorials for setting up Resiliency such as High Availability, Failover, and Disaster Recovery for the above application.
 - [refarch-cloudnative-resiliency](https://github.com/ibm-cloud-architecture/refarch-cloudnative-resiliency/tree/kube-int)   - The Resiliency Assets will be managed here
 - [refarch-cloudnative-kubernetes-csmo](https://github.com/ibm-cloud-architecture/refarch-cloudnative-kubernetes-csmo)   - The BlueCompute application end-to-end cloud service management for Kubernetes based deployment  

## Run the reference application in IBM Cloud

To run the sample applications you will need to configure your Bluemix environment for the Kubernetes and Microservices
runtimes.  

### Step 1: Environment Setup

#### Prerequisites

You must have a Bluemix account. The account is free and provides access to everything you need to develop, track, plan, and deploy apps. [Sign up for a trial of Bluemix](https://bluemix.net/registration). The account requires an IBMid. If you don't have an IBMid, you can create one when you register.


#### Get application source code

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

#### Deploy BlueCompute Community Edition to Local Minikube Cluster

We created a couple of handy scripts to deploy the Bluecompute Stack for you in your [Local Minikube Cluster](https://kubernetes.io/docs/tasks/tools/install-minikube/). Please run the following command.

```
$ ./install_bluecompute_ce.sh minikube
```

Once the actual install of Bluecompute takes place, it takes about 5-10 minutes to be fully deployed. So it might look like it's stuck, but it's not. Once you start to see output, look for the `Bluecompute was successfully installed!` text in green, which indicates that the deploy was successful and cleanup of jobs and installation pods will now take place. Please wait a minute or two to access the web app since some of the Microservices Pods are still initializing.

At the very end you will get a **URL** (i.e. http://192.168.99.100:31469) to access the Bluecompute Web App.    

![BlueCompute Detail](static/imgs/bluecompute_web_home.png?raw=true)  
You can reference [this link](https://github.com/ibm-cloud-architecture/refarch-cloudnative-bluecompute-web/tree/kube-int#validate-the-deployment) to validate the sample web application.  

Login Credentials: Once you are on the Bluecompute Web App, use the following test credentials to login:
- **Username:** user
- **Password:** passw0rd

That's it! **Bluecompute is now installed** in your Kubernetes Cluster. To see the Kubernetes dashboard, run the following command which will open a new browser window:

`$ minikube dashboard`

Then navigate to the **Services and discovery** section to see all the **Services** created by Bluecompute charts.

If you like to see **installation progress** as it occurs, use the `minikube dashboard` command to open a new browser window, then navigate to the `Jobs` section to see Installation jobs.

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

##### Delete Bluecompute Community Edition from Local Minikube Cluster
To delete the Bluecompute Stack from your Local Minikube Cluster, run the following script:

```
$ ./delete_bluecompute_ce.sh minikube
```

#### Deploy Bluecompute to Paid Cluster

Just like in the [Deploy Bluecompute to Lite Cluster](#deploy-bluecompute-to-lite-cluster) section, we created a couple of handy scripts to deploy the Bluecompute Stack for you. If you haven't done so, please [Create a New Bluemix Space](#create-a-new-space-in-bluemix) and [Create a Bluemix API Key](#create-a-bluemix-api-key). Then, run the following command:

```
# Supported Regions:
# ng
#  - (US South) - Default
# eu-de
#  - (Germany)

$ ./install_bluecompute.sh <cluster-name> <bluemix-space-name> <bluemix-api-key> <Optional:region>
```

Once the actual install of Bluecompute takes place, it takes about 10~15 minutes to be fully deployed. So it might look like it's stuck, but it's not. Once you start to see output, look for the `Bluecompute was successfully installed!` text in green, which indicates that the deploy was successful and cleanup of jobs and installation pods will now take place.

At the very end you will get a **URL** to access the Bluecompute Web App.
That's it! **Bluecompute is now installed** in your Kubernetes Cluster. To see the Kubernetes dashboard, run the following command:

`$ kubectl proxy`

Then open a browser and paste the following URL to see the **Services** created by Bluecompute charts:

  http://127.0.0.1:8001/api/v1/proxy/namespaces/kube-system/services/kubernetes-dashboard/#/service?namespace=default

If you like to see **installation progress** as it occurs, open a browser window and paste the following URL to see the Installation Jobs:

  http://127.0.0.1:8001/api/v1/proxy/namespaces/kube-system/services/kubernetes-dashboard/#/job?namespace=default

Be mindful that jobs come and go as new charts are getting installed.

**Login Credentials:** Once you are on the Bluecompute Web App, use the following test credentials to login:
- **Username:** user
- **Password:** passw0rd


##### Delete Bluecompute from Paid Cluster

To delete the Bluecompute Stack from your cluster, run the following script:

```
# Supported Regions:
# ng
#  - (US South) - Default
# eu-de
#  - (Germany)

$ ./delete_bluecompute.sh <cluster-name> <bluemix-space-name> <bluemix-api-key> <Optional:region>
```

## DevOps automation, Resiliency and Cloud Management and Monitoring

### DevOps
You can setup and enable automated CI/CD for most of the BlueCompute components via the Bluemix DevOps open toolchain. For detail, please check the [DevOps project](https://github.com/ibm-cloud-architecture/refarch-cloudnative-devops-kubernetes) .

### Cloud Management and monitoring
For guidance on how to manage and monitor the BlueCompute solution, please check the [Management and Monitoring project](https://github.com/ibm-cloud-architecture/refarch-cloudnative-kubernetes-csmo).

### Making Microservices Resilient
Please check [this repository](https://github.com/ibm-cloud-architecture/refarch-cloudnative-resiliency) on instructions and tools to improve availability and performances of the BlueCompute application.

### Secure The Application
Please review [this page](https://github.com/ibm-cloud-architecture/refarch-cloudnative/blob/master/static/security.md) on how we secure the solution end-to-end.


