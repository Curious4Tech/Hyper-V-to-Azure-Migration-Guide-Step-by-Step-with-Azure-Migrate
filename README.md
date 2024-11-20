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



![image](https://github.com/user-attachments/assets/992828a2-3098-4bbb-a9f5-736077be7ffc)



- **Verify Permissions**: Ensure your Azure account has the necessary permissions.

### Download and Configure the Azure Migrate Appliance
- **Download the Appliance**: Download the Azure Migrate appliance from the Azure portal.



![image](https://github.com/user-attachments/assets/02932575-38e1-4a43-b6b4-df9512e01b96)


- Discover section under **"Azure Migrate | Servers, databases, and web apps**." It provides a guide for discovering on-premises environments using the Azure Migrate appliance. Here are the key steps shown:

  . **Select Virtualization**: The servers are virtualized, with **"Yes, with Hyper-V**" chosen.

  . **Generate Project Key**: An appliance named **"mykey"** , and then click on **generate key** to generate a new key and then copy and save it, you will need it later.

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


- Follow the loging procedure, by providing the code and provide your Azure account credentials. At the end you will be successfully loged in. Now you need to wait up to 10 minutes before being able to continue with the next step. Now you're  successfully registered.


![image](https://github.com/user-attachments/assets/a3bf9691-d5ef-46cf-bf72-1d349682fa56)



### Manage credentials and discovery sources

- **Add credentials**: Click on **Add credentials** and provide your server admin credeantials and the click on **Save**.

    . **Source type** : Choose **`Hyper-V Host/ Cluster`**
  
    . **Friendly name** : Choose a name you want (e;g: **HypervServer**) it doesn't have obligatory to be the name of the host on which you Hyper-V is installed.
  
    . **Username** : Admin username (e.g; **Administrator**) of hsost machine where hyper-V server is installed
  
    . **Password** : admin password



![image](https://github.com/user-attachments/assets/c3b02da9-c9c7-4670-96d0-3e2de0dfe274)




- **Add Discovery** : Click on **Add discovery**, then clcik on **Add single item**. Now provide the following informations needed and then clcik on **Save**.
  
    . **Discovery soure** : Choose **`Hyper-V Host/ Cluster`**
  
    . **IP address/ FQDN** : your server domain name or your server Ip address
  
    . **Map credentrials** : Choose your previous server added



![image](https://github.com/user-attachments/assets/e35df6f9-75df-4e4f-bbbe-effb8fcd6ab3)

 
 - Successfully discovered. In case you have problem, allow the port **`5985`** in the firewall inboud rules.



![image](https://github.com/user-attachments/assets/fb298203-d0ca-4f7a-9209-6839cec9a5d2)


- You can also do the same for the sql server but it is optional for this demo. So I disabled this option for the sake of this demo.



![image](https://github.com/user-attachments/assets/1b956969-2e03-440e-b5ac-5b0f2520d427)




- Now you can click on **Start discovery** to start the discovery.



![image](https://github.com/user-attachments/assets/1c4a4195-0d3a-4ea5-adcb-1f30943fae0c)


- Now you need to wait untill the discovery to finish. After a successfully finished, you can go back to the Azure portal for the rest.



![image](https://github.com/user-attachments/assets/bbe477e0-cd2e-43b1-a806-e775a1768dd7)



### Assess Hyper-V VMs

- Go back to the Azure portal, then to **Azure migrate** and then your project to see the discovery.



![image](https://github.com/user-attachments/assets/aacedbaf-a58f-482b-a30d-ef6d12b57219)



- As indicated, you will click on **Assess** and choose **Azure VM** to start assessing.



![image](https://github.com/user-attachments/assets/19ecc78d-f51e-455b-8ff7-3aeb74f56b98)


- You need to create a group for you assessment, on the basics tab, click on **edit** just beside **assessment settings**



![image](https://github.com/user-attachments/assets/83127cf0-4ac9-41a4-a082-8830ed56537e)



- In the new windows that is going to open, choose the right detail informations for your migrating server including **Target settings, VM size , Pricing, Azure Hybrid Benefit  and Security**, then click on **Save**.



![image](https://github.com/user-attachments/assets/4cbad94f-0196-4465-aca8-c3c9f6e4633b)




- **Selected servers to access** : Create a new group by giving it a name, choose your appliance. Make sure your server that you want to migrate is checked and then proceed.



![image](https://github.com/user-attachments/assets/53f8d2b4-54b9-435f-bef5-6fb2e44e4db9)



- Verify and create assessment : Review to see if everything is correct before clicking on **Review + create assessment**. If there is any change you want to make, you can clcik on **Previous**.



![image](https://github.com/user-attachments/assets/554a4c1f-53c6-4ada-88a7-5dc4adc72217)



- After successfully assessment, your server is ready as you can.



![image](https://github.com/user-attachments/assets/4bc91236-edc2-4d91-841a-464a2a2c9d4d)



- If you clcik on the newly created group you should see something like this.



![image](https://github.com/user-attachments/assets/af48a175-2ab7-405c-a792-cfd7f33ad4d4)


- Click on **Build Business case** 



![image](https://github.com/user-attachments/assets/bf37a599-dea3-421c-83f5-f1897f7666da)


- Now provide all the infos depending on your needs. And clcik on **Build Buisiness case**. After that you have to wait for some minutes before your plan to be ready.


![image](https://github.com/user-attachments/assets/a3fcaf57-b8e8-431f-8674-ebfb108ac30a)


- Plan successfully built


![image](https://github.com/user-attachments/assets/68fb1922-e1ff-4cb7-9ce6-5260fd182924)


- Migrate, by click on migrate, 



![image](https://github.com/user-attachments/assets/dcf71724-c8ff-4d4e-9265-427dc37e63f7)


- Provide all the informations based on your need and then click on **Create a resources**



![image](https://github.com/user-attachments/assets/268819da-9c24-4566-9382-069689405747)


- Now download these two files


![image](https://github.com/user-attachments/assets/f546f10f-0693-4831-958a-7c492402dd5b)


- **Test Functionality**: Test the functionality of the migrated VMs to ensure everything is working correctly.
- **Clean Up**: Clean up any resources that are no longer needed on the Hyper-V host.



![image](https://github.com/user-attachments/assets/6cf2e4ac-da4a-4624-a675-548f9fb575aa)



## Additional Resources
- [Azure Migrate Documentation](https://learn.microsoft.com/en-us/azure/migrate/tutorial-migrate-hyper-v)

