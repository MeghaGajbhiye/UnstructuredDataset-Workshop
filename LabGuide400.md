Updated: December 10, 2018



# Unstructured datasets in Autonomous Database

## JSON data has often been stored in NoSQL databases such as Oracle NoSQL Database and Oracle Berkeley DB. These allow for storage and retrieval of data that is not based on any schema, but they do not offer the rigorous consistency models of relational databases.
## To compensate for this shortcoming, a relational database is sometimes used in parallel with a NoSQL database. Applications using JSON data stored in the NoSQL database must then ensure data integrity themselves. Plus, SQL and relational databases provide flexible support for complex data analysis and reporting, as well as rock-solid data protection and access control. This is typically not the case for NoSQL databases, which have often been associated with schemaless development with JSON in the past. 
## Native support for JSON by Oracle Database obviates such workarounds. It provides all of the benefits of relational database features for use with JSON, including transactions, indexing, views and declarative querying, for example in Oracle Database you can use SQL to join JSON data with relational data. And you can project JSON data relationally, making it available for relational processes and tools. You can also query, from within the database as well as JSON data that is stored outside Oracle Database in an external table.
## And, you can access JSON data stored in the database the same way you access other database data, including using OCI, .NET, and JDBC.

## In Oracle Database, JSON data is stored using the common SQL data types VARCHAR2, CLOB, and BLOB (unlike XML data, which is stored using abstract SQL data type XMLType). 

## In general, you will perform the following tasks when working with JSON data in Oracle Database: 
1. You create internal table, which is the traditional way – where data is stored internally within the database or you create External tables which allow Oracle to query data that is stored outside the database in flat files. You can store these files in either Oracle’s Object Storage, Amazon S3 or Microsoft Azure Blob.
2. create a JSON column with an ”is json” check constraint, Oracle recommends that you use an is_json check constraint to ensure that column values are valid JSON instances 
3. insert JSON data into the column, and 
4. query the JSON data.

## You can also create a database table of JSON data from the content of a JSON dump file.

## Introduction

This lab guide will walk you through the process of configuring a Compute Linux Instance for Datapump.

**_To log issues_**, click here to go to the [github oracle](https://github.com/oracle/learning-library/issues/new) repository issue submission form.

## Objectives

- Download Instant Client.
- Transfer files to Compute instance.
- Login to Linux instance from command prompt.
- Unzipping packages.
- Configuring environmant variables.


## Required Artifacts

- An oracle cloud account with Autonomous Data Warehouse Cloud Service.
- FileZilla or any SFTP software for windows.

### **STEP 1**: Download Instant Client.

In this step you will download **Instant Client** for ADWC.

- Go to this link : https://www.oracle.com/technetwork/database/database-technologies/instant-client/overview/index.html
    
  Click on **Downloads**.

  ![](images/datapump/compute21.png)    

- Select **Instant Client for Linux x86-64**. Click on **Accept Licence Agreement**. Navigate to **Version 18.3.0.0.0** section, then under **Base - one of these packages is required** section, click on **instantclient-basic-linux.x64-18.3.0.0.0dbru.zip**. It will download this package. Under **Tools - optional packages** section, click on **instantclient-tools-linux.x64-18.3.0.0.0dbru.zip**. This will download the package required for data pump.

  ![](images/datapump/compute22.png)

- For quick access, copy paste both the zip files to **DemoADWC** directory that you have created in Lab 2. 
    
### **STEP 2**: Transfer files to Compute instance.

- Go to your Oracle Cloud console. Click on your compute Linux instance and jot down the public IP address of the instance.  
    
    ![](images/datapump/compute15.png)

- **For Mac users**: We will transfer a few files to the compute instance. 
  Navigate to the **DemoADWC** directory where you have downloaded the wallet and instant client. 
  
  Type the following command from the command line:
 
  **scp -i {your folder location}/{wallet file name}.zip opc@{IP address}:{wallet file name}.zip**
  
  **scp -i {your folder location}/{instantclient basic package file name}.zip opc@{IP address}:{instantclient basic package file name}.zip**
  
  **scp -i {your folder location}/{instantclient tool package file name}.zip opc@{IP address}:{instantclient tool package file name}.zip**
    
- **For windows user**: Open any SFTP software. I am using FileZilla, so I will explain the steps through FileZilla.
  Click on **FileZilla** and then **Settings**. 
    
    ![](images/datapump/compute16.png)
    
- under **Connections**, click on **SFTP** . Upload your private key by clicking on **Add key file...**

    ![](images/datapump/compute17.png)
    
- Click on **File**, and **Site Manager**.

    ![](images/datapump/compute18.png)
    
- Click on **New Site** and name it as **DataPump**. Select **Protocol** as **SFTP**. Enter the Compute's **Public IP Address** in **Host**. Enter **opc** as **User**. Leave **Password** blank and Click on **Connect**.

    ![](images/datapump/compute19.png)

- A pop-up of **Unknown host key** will appear. Click on **Always trust this host...** and click **Ok**.

    ![](images/datapump/compute20.png)    

- Make sure that you are connected to the instance. Look at the top-left, status should show **Connected to (Your IP Address)**
    
    ![](images/datapump/compute23.png)
 
- Drag and drop **zip format of wallet** (Downloaded in step 4), **instant client basic and tool package** (Downloaded in step 5) to the Linux instance through FIleZilla (Remote site). 

    ![](images/datapump/compute24.png)
  
### **STEP 3**: Login to Linux instance from command prompt.

- Set these parameters:
    
    - **your_private_key** : The filename of your private key. Make sure that you are in the same folder as your private key or else enter the file path. 
    - **public_ip_address** : Oracle compute's IP address. (The one copied in step 2)
    
    Open a command prompt and type **ssh -i your_private_key opc@public_ip_address**. 
    It will ask **Are you sure you want to continue connections**, type **yes**

    ![](images/datapump/compute25.png)
    

### **STEP 4**: Unzip packages.

- After logging in to the compute instance, if you do **ls**, you will be able to see all the zip files that we have transferred. 

- Make a directory called **oracle** by typing the following command **mkdir oracle**. (Check the screenshot below)

- Unzip the basic and tool package in the folder **oracle**. 
  
  Parameters to change in command-  
  **instantclient-basic-package**: instant client basic zip file name.
  **instantclient-tool-package**: instant client tool zip file name.
  
  Type following command in command line: 
  
  **unzip instantclient-basic-package.zip -d oracle/**
  
  **unzip instantclient-tool-package.zip -d oracle/**


  ![](images/datapump/compute26.png)
    
- Unzip the wallet in the folder  **/oracle/instantclient_18_3/network/admin** by typing the following in command line:
  
  **unzip wallet_file_name.zip -d /home/opc/oracle/instantclient_18_3/network/admin/**
  
  ![](images/datapump/compute28.png)
    
### **STEP 5**: Configure environment variables.

- Type following lines in command prompt:

    **export ORACLE_HOME=/home/opc/oracle/instantclient_18_3**

    Makes sure you echo the variable and check if all parameters is set.    
    
    **export LD_LIBRARY_PATH="$ORACLE_HOME""**
    
    **export PATH="$ORACLE_HOME:$PATH"**
       
    ![](images/datapump/compute29.png) 
    
    **export TNS_ADMIN=/home/opc/oracle/instantclient_18_3/network/admin**

- Let's navigate to **/home/opc/oracle/instantclient_18_3** and check if **impdp** is configured

    ![](images/datapump/compute30.png)
    
 