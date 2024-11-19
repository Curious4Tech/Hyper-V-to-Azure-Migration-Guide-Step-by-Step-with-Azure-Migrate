# Hyper-V-to-Azure-Migration-Guide-Step-by-Step-with-Azure-Migrate
Comprehensive guide to migrating servers from Hyper-V to Azure using Azure Migrate. Covers pre-migration planning, Azure setup, replication, testing, and post-migration configuration. Ideal for IT professionals and cloud engineers transitioning workloads to Azure.


# **Server Migration from Hyper-V to Azure**

This guide provides a detailed step-by-step process for migrating a server from Hyper-V to Microsoft Azure using Azure Migrate.

---

## Table of Contents
1. [Introduction](#introduction)
2. [Prerequisites](#prerequisites)
3. [Step-by-Step Guide](#step-by-step-guide)
   - [Prepare Azure](#prepare-azure)
   - [Download and Configure the Azure Migrate Appliance](#download-and-configure-the-azure-migrate-appliance)
   - [Discover and Assess Hyper-V VMs](#discover-and-assess-hyper-v-vms)
   - [Install Required Agents](#install-required-agents)
   - [Enable Replication](#enable-replication)
   - [Perform Test Migration](#perform-test-migration)
   - [Perform Final Migration](#perform-final-migration)
4. [Post-Migration Tasks](#post-migration-tasks)
5. [Additional Resources](#additional-resources)

## Introduction
This guide provides detailed steps to migrate a server from Hyper-V to Azure using Azure Migrate.

## Prerequisites
Before starting, ensure you have:
- An active Azure subscription.
- Permissions to create VMs and write to Azure managed disks.
- Access to the Hyper-V host and VMs you want to migrate.

## Step-by-Step Guide

### Prepare Azure
- **Create an Azure Migrate project**: In the Azure portal, create a new project under the "Migration and Modernization" tool.



  ![image](https://github.com/user-attachments/assets/06703932-564d-467d-bd69-ed5fe3e2d643)


- Provide detailled information
    .  **Sucbscription**
    .  **Resource group**
    .  **Project name**
    .  **Geography**
    .  **Connectivity method**
- Click on **Create** to finish your project creation

  ![image](https://github.com/user-attachments/assets/e2c7c0eb-7bb0-4a8b-a442-f61a5d3e0f0d)



- **Verify Permissions**: Ensure your Azure account has the necessary permissions.

### Download and Configure the Azure Migrate Appliance
- **Download the Appliance**: Download the Azure Migrate appliance from the Azure portal.


  ![image](https://github.com/user-attachments/assets/02932575-38e1-4a43-b6b4-df9512e01b96)


- Discover section under **"Azure Migrate | Servers, databases, and web apps**." It provides a guide for discovering on-premises environments using the Azure Migrate appliance. Here are the key steps shown:

  . **Select Virtualization**: The servers are virtualized, with **"Yes, with Hyper-V**" chosen.

  . **Generate Project Key**: An appliance named **"mykey"** , and then click on **generate key** to generate a new key and then copy it, you will need that later.

  . **Download Appliance**: There are options to download either a .VHD file (12GB) or a .zip file (500MB), with the download (here am downloading .zip, so I will use powershell for the installation process).


![image](https://github.com/user-attachments/assets/fbe688d9-e459-48f5-89c8-bd0dfc00247f)


- **Install the Appliance**: Install the appliance on a Hyper-V host.


   . Unzip the file:


![image](https://github.com/user-attachments/assets/953e1376-35e1-4e79-a175-0612854e4d1d)


  . Open the powershell and move to the path where you unziped the appliance installation folder and run: **`.\AzureMigrateInstaller.ps1`**


![image](https://github.com/user-attachments/assets/aa6487dd-8237-4c87-b922-24a1b0441d76)

  
- **Register the Appliance**: Register the appliance with your Azure Migrate project.


![image](https://github.com/user-attachments/assets/78d180e5-c81e-455b-ae8c-a91fbb32f147)


- Follow the powershell prompt and I read cearfully to make the right choices.
  . After successfully installation copy the url provided and  paste it on the web browser and then continue the procedure


![image](https://github.com/user-attachments/assets/3d7f107c-5a01-4c34-afa0-3e0f71f6dc59)


### Discover and Assess Hyper-V VMs
- **Discover VMs**: Use the Azure Migrate appliance to discover the Hyper-V hosts and VMs.

  . Wait for the pre requisites to commance


![image](https://github.com/user-attachments/assets/04581157-ddfb-4702-b4ab-ad1c395c8cad)


  . Provide your project key, the key you have created before and then click on **Verify**. You have to wait for some minutes.


![image](https://github.com/user-attachments/assets/8622f75b-bb10-4b08-880c-908c270189d7)


  . After some minutes, you will have a pop-pup, just clcik **Refresh**



![image](https://github.com/user-attachments/assets/a4984372-0bf8-49f5-a157-8ee09dfc913a)


- Now you need to login with your Azure account credentials. Click on **Login**


![image](https://github.com/user-attachments/assets/4aba956b-7358-4a89-ad64-0fc44429109a)


- Click on **copy and login** on the new pop-pup windows that is gonna open.


![image](https://github.com/user-attachments/assets/acee1a46-479c-490c-8207-94438f1f0551)


- Follow the loging procedure, by providing the code and provide your Azure account credentials. At the end you will be successfully loged in. Now you need to wait up to 10 minutes before being able to continue with the next step.


![image](https://github.com/user-attachments/assets/e8ae8572-8439-457f-ae56-0af14d1ca730)


- **Create an Assessment**: Create an assessment to review the readiness and cost of migrating the VMs to Azure.

### Install Required Agents
- **Install Mobility Service**: Install the Mobility Service on the VMs to enable deeper discovery and dependency analysis.

### Enable Replication
- **Enable Replication**: Enable replication for the VMs to start copying data to Azure.
- **Monitor Progress**: Monitor the replication progress to ensure everything is running smoothly.

### Perform Test Migration
- **Test Migration**: Perform a test migration to ensure everything works as expected without any data loss.
- **Review Results**: Review the test migration results and make any necessary adjustments.

### Perform Final Migration
- **Final Migration**: Once the test migration is successful, perform the final migration with zero data loss.
- **Verify Network and DNS Settings**: Verify the network and DNS settings of the migrated VMs in Azure.

## Post-Migration Tasks
- **Test Functionality**: Test the functionality of the migrated VMs to ensure everything is working correctly.
- **Clean Up**: Clean up any resources that are no longer needed on the Hyper-V host.

## Additional Resources
- [Azure Migrate Documentation](https://learn.microsoft.com/en-us/azure/migrate/tutorial-migrate-hyper-v)

