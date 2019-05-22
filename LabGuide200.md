Updated: December 10, 2018

## Introduction

This lab guide will walk you through the process of creating Autonomous Data Warehouse cloud service. We will also crreate a user in Oracle Machine Learning (OML). We will then upload the dataset in Object StoraGE and will import the notebook in OML.

**_To log issues_**, click here to go to the [github oracle](https://github.com/oracle/learning-library/issues/new) repository issue submission form.

## Objectives

- Create an Autonomous Data Warehouse Cloud Service.
- Download Dataset and notebook.
- Connect and create a user in Oracle Machine Learning (OML).
- Import UnstructuredDataset Notebook in OML. 
- Load data in Object Storage.


## Required Artifacts

- An oracle cloud account with Autonomous Data Warehouse Cloud Service.

### **STEP 1**: Create Autonomous Data Warehouse Cloud Service (ADWC).


- Login into your cloud account. Click on **Menu** and click on **Autonomous Data Warehouse.**

    ![](images/UnstructuredData/compute8.png)

- Click on **Create Autonomous Data Warehouse**.

    ![](images/UnstructuredData/compute9.png)

- On Details screen, select the **Compartment**, enter **Display Name and Database Name**. Keep the **CPU Core Count and Storage** as **1**. Finally enter the **Password** and **Confirm Password**.

    - **Note** : Make sure your password doesn't have **"@"**. It might create a problem later.
    
    ![](images/UnstructuredData/compute10.png)
    
    ![](images/UnstructuredData/compute10-2.png)

- Select a **License Type** and click on **Create Autonomous Data Warehouse**.
    
    ![](images/UnstructuredData/compute11.png)
    
### **STEP 2**: Download Dataset and notebook.  
    
- For dataset, download the following zip [Datafiles](images/UnstructuredData/DataFiles.zip)

- For Unstructured Dataset notebook, download the following [UnstructuredDataset](images/UnstructuredData/UnstructuredDataset.json)


### **STEP 3**: Create a user in Oracle Machine Learning (OML) and connect to it.

- Once your ADWC instance is avaiable, click on the ADWC instance that you have just created. Then Click on **Service Console**. 

    ![](images/UnstructuredData/serviceconsole.png)

- Then click on **Administration** and then **Manage Oracle ML Users**.

    ![](images/UnstructuredData/administration.png)
    
    ![](images/UnstructuredData/managemlusers.png)
    
- Click on **Create** under Users

    ![](images/UnstructuredData/createomluser.png)

- Create a user. Give **first name, last name, Email Address** and assign a password by unchecking **Generate password and email account.....**
    
    ![](images/UnstructuredData/createuser.png)

- Click on the home button on the top right corner of the home page 

    ![](images/UnstructuredData/homeoml.png)

- Login as the user you just created. 

    ![](images/UnstructuredData/loginoml.png)
  
    
### **STEP 4**: Import UnstructuredDataset Notebook in OML. 

- After login to OML, click on **Notebooks**.
    
    ![](images/UnstructuredData/notebook.png)

### **STEP 5**: Load data in Object Storage. 


- **Navigate to Object Storage**

    - From the Autonomous Data Warehouse console, pull out the left side menu from the top-left corner and select **Object Storage**. To revisit signing-in and navigating to ADW, please see Lab 1.

      ![](images/300/snap0014294.jpg)

      To learn more about the OCI Object Storage, refer to its <a href="https://docs.us-phoenix-1.oraclecloud.com/Content/GSG/Tasks/addingbuckets.htm" target="_blank">documentation</a> .

    - You should now be on the **Object Storage** page. Choose the compartment in the **Compartment** drop-down if it is not already chosen.
    ![](images/300/snap0014298.jpg)

- **Create a Bucket for the Object Storage**

   In OCI Object Storage, a bucket is the terminology for a container of multiple files.

    - Click the **Create Bucket** button:

      ![](images/300/snap0014299.jpg)

    - Name your bucket **UnstructuredDataset** and click the **Create Bucket** button.

      ![](images/UnstructuredData/UnstructuredDS_OS.png)

- **Upload Files to Your OCI Object Store Bucket**

    - Click on your **bucket name** to open it and then click on the **Upload Objects** button:

      ![](images/UnstructuredData/upload.png)

    - Using the browse button or select all the files downloaded in the earlier step, click Upload and wait for the upload to complete:

    ![](images/300/snap0014303.jpg)

-   Repeat this for all the dataset files you downloaded for this lab.

-   The end result should look like this with all files listed under Objects:

    ![](images/UnstructuredData/endresult.png)

 
