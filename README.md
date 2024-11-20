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



![image](https://github.com/user-attachments/assets/02f182b0-d051-4c7d-9ee3-b5c3effb09f2)



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


- Follow the powershell prompt and I read cearfully to make the right choices.

- After successfully installation copy the url provided and  paste it on the web browser and then continue the procedure



![image](https://github.com/user-attachments/assets/af6add27-fc75-4fee-b554-55303becc60d)




### Set up prerequisites

- **Discover VMs**: Use the Azure Migrate appliance to discover the Hyper-V hosts and VMs.

  . Accept the terms of use


![image](https://github.com/user-attachments/assets/16e1527b-a9f4-4ca2-a219-60749c2a5fb1)


  . Provide your project key, the key you have created before in the Azure portal and then click on **Verify**. You have to wait for some minutes (up to 5 minutes).



![image](https://github.com/user-attachments/assets/f5aa8357-eeb8-48dd-ae7e-50a3c66facae)


  
  . After some minutes, you will have a pop-pup, just clcik **Refresh**



![image](https://github.com/user-attachments/assets/a4984372-0bf8-49f5-a157-8ee09dfc913a)


- Now you need to login with your Azure account credentials. Click on **Login**


![image](https://github.com/user-attachments/assets/4aba956b-7358-4a89-ad64-0fc44429109a)


- Click on **copy code and Login** on the new pop-pup windows that is gonna open.



![image](https://github.com/user-attachments/assets/68515337-c031-4080-9abb-963fa71cc88f)


- Follow the loging procedure, by providing the code and provide your Azure account credentials. At the end you will be successfully loged in. Now you need to wait up to 10 minutes before being able to continue with the next step.


![image](https://github.com/user-attachments/assets/e8ae8572-8439-457f-ae56-0af14d1ca730)


### Manage credentials and discovery sources

- **Add credentials**: Click on **Add credentials** and provide your server admin credeantials and the click on **Save**.

    . **Source type** : Choose **`Hyper-V Host/ Cluster`**
  
    . **Friendly name** : Host name where you Hyper-V is installed
  
    . **Username** : Administrator
  
    . **Password** : administrator password



![image](https://github.com/user-attachments/assets/37e65aa8-283f-42f0-a68b-31da6644c2ea)


- **Add Discovery** : Click on **Add discovery**, then clcik on **Add single item**. Now provide the following informations needed and then clcik on **Save**.
  
    . **Discovery soure** : Choose **`Hyper-V host/ Clusters`**
    . **IP address/ FQDN** : your server domain name or your server Ip address
    . **Map credentrials** : Choose your previous server added


![image](https://github.com/user-attachments/assets/cdf3f3c9-a388-4454-b105-e222b447ff5d)


- Successfully discovered. In case you have problem, allow the port **`5985`** in the firewall inboud rules.


![image](https://github.com/user-attachments/assets/9cf8ec6c-31ac-49d0-bd59-6b1f2752cc08)


- You can also do the same for the sql server but it is optional for this demo.



![image](https://github.com/user-attachments/assets/437164f4-3d71-4e4f-b16e-bdfe615f6b04)



- Now you can click on **Start discovery** to start the discovery.



![image](https://github.com/user-attachments/assets/1c4a4195-0d3a-4ea5-adcb-1f30943fae0c)


- Now you need to wait untill the discovery to finish. After a successfully finished, you can go back to the Azure portal for the rest.


![image](https://github.com/user-attachments/assets/e679932e-63ed-47f0-8dfe-91022bbf4cf4)



### Assess Hyper-V VMs

- Go back to the Azure portal, then to **Azure migrate** and then your project to see the discovery.


![image](https://github.com/user-attachments/assets/9e784f96-e0d4-4100-9bf9-dc8bd987e11c)


- As indicated, you will click on **Assess** and choose **Azure VM** to start assessing.



![image](https://github.com/user-attachments/assets/19ecc78d-f51e-455b-8ff7-3aeb74f56b98)


- You need to create a group for you assessment, on the basics tab, click on **edit** just beside **assessment settings**


![image](https://github.com/user-attachments/assets/82ccf697-7933-42a1-a42c-72da723b37b9)


- In the new windows that is going to open, choose the right detail informations for your server including location , size, performance, storage  and so on and  then click on **Save**.



![image](https://github.com/user-attachments/assets/c27f5b41-7010-496e-9993-088f8486b941)


- Selected server to access : Create a new group by giving it a name, choose your appliance. Make sure your server that you want to migrate is checked and then proceed.



![image](https://github.com/user-attachments/assets/b0783606-d062-456e-ac68-70ac9ba12e01)


- Verify and create assessment : Review to see if everything is correct before clicking on **Review + create assessment**. If there is any change you want to make, you can clcik on **Previous**.



![image](https://github.com/user-attachments/assets/c257f44e-c8a7-4874-a389-aa227ba7699e)


- After successfully creation your server is ready as you can



![image](https://github.com/user-attachments/assets/e9a62277-5a88-46b6-8c23-66176766d996)


- If you clcik on the newly created group you should see something like this.


![image](https://github.com/user-attachments/assets/bbb47dce-9263-44e7-aac0-1f9d0bc1acfe)




## Post-Migration Tasks
- **Test Functionality**: Test the functionality of the migrated VMs to ensure everything is working correctly.
- **Clean Up**: Clean up any resources that are no longer needed on the Hyper-V host.



![image](https://github.com/user-attachments/assets/6cf2e4ac-da4a-4624-a675-548f9fb575aa)



## Additional Resources
- [Azure Migrate Documentation](https://learn.microsoft.com/en-us/azure/migrate/tutorial-migrate-hyper-v)

