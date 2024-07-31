# End to End Tokyo Olympic Data Engineer Project Using Microsoft Azure
![image](https://github.com/user-attachments/assets/dfe28e59-a3f8-4076-9e41-5921dc749c13)

In this project, we will perform data analysis on the Olympic dataset and uncover insights such as:

1. Top 20 countries in terms of Number of participants
2. Top 20 countries in terms of Number of coaches
3. Top countries in terms of Number of medals
4. Total Participants in each Discipline
5. Density of Countries in 2021
6. Country-wise Gold medals, Silver medals, Bronze medals
7. Rank VS Total Medal

Download the dataset from my GitHub: [Tokyo Olympics Dataset](https://github.com/tanya88099/OlympicData/tree/main/Dataset)

## Tokyo Olympics Dataset Overview

**Dataset Scope:** This dataset provides comprehensive information about the athletes, coaches, teams, and their performance at the 2021 Tokyo Olympics (held in 2020). It encompasses details about over 11,000 athletes participating in 47 disciplines across 743 teams.

**Dataset Components:**
The dataset is comprised of five primary files:

- **Athletes.csv:** Contains individual athlete information, including their name, the country they represent (NOC), and the discipline they compete in.

  ![image](https://github.com/user-attachments/assets/0116f455-c04c-440a-a8bf-36169b9fee30)

- **Coaches.csv:** Lists coaches with their respective countries, disciplines, and associated events.

  ![image](https://github.com/user-attachments/assets/8644a999-1d31-472c-b4b3-ebfdefdd3367)

- **EntriesGender.csv:** Details the gender distribution of participants across disciplines and countries.

  ![image](https://github.com/user-attachments/assets/f398f4b0-47e2-43b6-9e80-78613a757f4a)

- **Medals.csv:** Outlines the medal tally for each country as of July 29, 2021.

  ![image](https://github.com/user-attachments/assets/295811d1-b0b2-44c7-8c1e-be9a74919b73)

- **Teams.csv:** Provides information about participating teams, including their country, event, and discipline.

  ![image](https://github.com/user-attachments/assets/bc5ba51a-ef13-47b1-8dad-9d97800c09b2)


## Let's Begin

## Table of Contents
1. [Introduction](#introduction)
2. [Tools and Technologies](#tools-and-technologies)
3. [Project Workflow](#project-workflow)
4. [Azure Cloud Architecture](#azure-cloud-architecture)
5. [Setting Up the Environment](#setting-up-the-environment)
6. [Contributing](#contributing)
7. [License](#license)

## Introduction

If you're new to Azure cloud services, this documentation will help you understand the basic concepts before diving into our Tokyo Olympic data analysis project. The project uses Azure's powerful suite of tools to perform end-to-end data analytics.

## Tools and Technologies

This project utilizes the following Azure services:

1. **Azure Data Factory**: A cloud-based data integration service that enables you to create, schedule, and orchestrate data pipelines.
2. **Data Lake Gen 2**: A scalable data lake solution for big data analytics, providing secure and massively parallel data processing capabilities.
3. **Synapse Analytics**: An integrated analytics service combining big data and data warehousing to provide comprehensive insights.
4. **Azure Databricks**: A collaborative Apache Spark-based analytics platform for advanced analytics, machine learning, and data exploration.

  ![image](https://github.com/user-attachments/assets/6de6d980-46ea-4c28-aabb-f5fe9bb612ed)

## Project Workflow

The project follows these steps:

1. **Data Collection**: Gather data from various sources.
2. **Data Integration**: Use Azure Data Factory to integrate and save the raw data into Data Lake Gen 2.
3. **Data Transformation**: Transform the data using Azure Databricks and save the processed data back into Data Lake Gen 2.
4. **Data Analysis**: Analyze the data using Azure Synapse Analytics and visualize the results with Power BI, Looker Studio, or Tableau.

## Azure Cloud Architecture
  
  ![image](https://github.com/user-attachments/assets/87df14ec-2684-4ba9-b87e-37d41d26616c)

### Project Initialization

**Creating an Azure Storage Account**

1. **Navigate to the Azure Portal**: Visit the Azure home page and click on "Create a resource (+)".

   ![image](https://github.com/user-attachments/assets/5e6f4dc1-109b-4e86-8c51-7eae20bc4c39)

3. **Create Storage Account**: Select "Storage Account" from Popular Azure Services and click "Create".

   ![image](https://github.com/user-attachments/assets/331ee611-1d63-47e2-bec8-c51237379bdb)

5. **Configure Account Details**:
   - Select your subscription.
   - Create a resource group.
   - Provide a unique storage account name.
   - Select performance, redundancy, and region options.
   - Click "Next".

  ![image](https://github.com/user-attachments/assets/1f4a5045-a525-40fe-90ee-7fac1b65e175)

   **Note**: The storage account name must be unique across the region.

7. **Advanced Settings**:
   - Configure the hierarchical namespace, blob storage, security, and Azure Files settings as required.
   - For frequent data access, choose the Hot tier.
   - Enable the “Hierarchical namespace” for directory-like storage organization.
   ![image](https://github.com/user-attachments/assets/a6771a30-bc46-420c-905f-64613ea756ba)
   ![image](https://github.com/user-attachments/assets/7a435553-c920-47ab-ab9a-f4a9fc7a5916)

8. **Networking Settings**:
   - Enable public access from all networks.
   - Configure network routing.
   - Click "Next".
    ![image](https://github.com/user-attachments/assets/f7bf8534-3c40-4ec9-900f-b8e1c9ef2426)


9. **Review and Create**: Proceed through the validation steps to the “Review + create” tab. If the validation passes, click "Create". Deployment will take approximately 2 minutes. After completion, click "Go to resource".
    ![image](https://github.com/user-attachments/assets/ac1ac162-876f-49a0-8eea-c08d833ad3c1)



10. **Creating Containers**:
   - Scroll down the left-side menu and click on "Data Storage -> Container".
   - **Why Containers?**:
     - **Containers (Blob Storage)**: Virtual folders for grouping blobs (files), ideal for storing unstructured data like images, videos, and large files.
     - **File Shares (Azure Files)**: Managed file shares accessible via SMB, suitable for collaborative file access.
     - **Queues (Azure Queue Storage)**: A message queuing service following FIFO order, useful for asynchronous task handling.
     - **Tables (Azure Table Storage)**: A schemaless NoSQL store for large amounts of structured data with flexible schemas.

   Based on our requirements for creating directories to store raw and transformed data, we'll use containers.

11. **Creating Directories**:
   - Click on "+ Container" to create a new container.
     ![image](https://github.com/user-attachments/assets/d75b79d0-275e-47a2-ae0e-9523f7a90a88)

   - Provide a container name and click "Create".
   - Click on the newly created container and create two directories by clicking “+ Add Directory” for raw data and transformed data.
     ![image](https://github.com/user-attachments/assets/64342854-24ae-45b3-9fc3-99dade2bc13b)


### Setting Up Data Factory

1. **Search for Data Factory**: Use the search bar to find "Data Factory" and open it in a new tab.

     ![image](https://github.com/user-attachments/assets/b2baca5f-faec-4cdb-856a-6c42d9b4be02)
   
2. **Create Data Factory**:
   - Select the resource group.
   - Provide an instance name.
   - Proceed to the “Review + create” tab without changing the git config or networking settings.

     ![image](https://github.com/user-attachments/assets/7faee8e2-0ea6-498b-a944-b15289546a85)

   - After validation, click "Create". Deployment will begin.
   - Upon completion, click "Go to resources".

     ![image](https://github.com/user-attachments/assets/aee039ac-fa55-4445-97fb-7228a6da4d7b)


3. **Launch Studio**: Click on "Launch Studio" to open the Data Factory studio in a new tab.

   ![image](https://github.com/user-attachments/assets/54e4c847-2d61-4019-a376-8781bce658b1)

## Azure Data Factory Functionalities

In Azure Data Factory (ADF), the terms Author, Monitor, Manage, and Learning Center refer to different functionalities within the service:

### Author
This refers to the process of creating and defining data pipelines. ADF provides a visual interface and code editing capabilities to build data pipelines that integrate, transform, and move data between various sources and destinations. Users designated as "authors" have the permissions to create, edit, and publish data pipelines within ADF.

### Monitor
This refers to the ability to track the execution status and performance of data pipelines. ADF offers a monitoring interface that allows users to view pipeline runs, identify errors or failures, and analyze execution logs. This is crucial for ensuring data pipelines are functioning correctly and meeting processing requirements.

### Manage
This encompasses a broader set of administrative tasks related to data factory resources. It includes activities like:
- Managing data connections: Defining and configuring connections to various data sources and sinks (e.g., databases, cloud storage accounts) used by pipelines.
- Managing triggers: Setting up schedules or events to trigger pipeline execution automatically.
- Managing parameters: Defining reusable variables used within pipelines for customization and configuration.
- Managing user permissions: Granting access to different ADF functionalities for various users based on their roles.
- Managing access control (IAM): Configuring access control settings to determine who can access and manage data factory resources.

### Learning Center
This is a resource within ADF that provides documentation, tutorials, and other learning materials to help users of various skill levels understand and utilize the service effectively. It can be used by authors, monitors, and managers alike to learn new functionalities, explore best practices, and find solutions to common challenges.

### Summary
- **Authoring** focuses on creating data pipelines.
- **Monitoring** involves tracking pipeline execution and performance.
- **Managing** covers broader administrative tasks within the data factory.
- **Learning Center** provides educational resources for ADF users.

These functionalities work together to enable users to design, execute, monitor, and manage data pipelines effectively within Azure Data Factory.

### Creating Data Pipelines

1. **Go to the Author Tab**: Click on "pipeline" under the pipeline section.

    ![image](https://github.com/user-attachments/assets/c5e55e0d-1844-4a14-ae8d-dcf045cd5443)
    ![image](https://github.com/user-attachments/assets/c7644e3b-75fa-4dd3-916c-2af2169de623)

3. **Name the Pipeline**: On the right side, it will ask for a pipeline name. Provide a name and click on "Move and transform".

   ![image](https://github.com/user-attachments/assets/caabde18-0eaa-4cde-a60b-4ecaa9f76c13)
   ![image](https://github.com/user-attachments/assets/0eb9d1c4-d026-4325-831f-784b7e6af69c)

   **Note**: No coding is required here to transform the data; you only need to perform Drag and Drop operations and link the tables.
   Name : Athletes and go to “Source”(Source means from where the data is coming and which format) and click on “+” icon.

   ![image](https://github.com/user-attachments/assets/b188fa8c-1499-4257-a88a-0b5f61f9d0ce)
   
  Type HTTP in search bar and click on it,  because our data is picking up from git hub and I have only raw data link.
  
  ![image](https://github.com/user-attachments/assets/25f96333-050c-4281-a9ae-619bb9571ed8)
  
  Select “DelimitedText” click on Continue.
  
  ![image](https://github.com/user-attachments/assets/f86075ce-e0b8-45dd-b1d6-40ee7dbc2a30)

  Set the name of properties (for example: Athletes) and click on linked service->New.
  Change the HTTP server name like : AthletesHTTP
  Use Athletes Link to put in the base URL, use Authentication type “Anonymous” and click on create.
  https://raw.githubusercontent.com/tanya88099/OlympicData/main/Dataset/Athletes.csv
  Back to the Set Properties click on Import Schema:None (because no Schema is saved in the Data factory from advance.).Click on “OK”. Click on Preview to check the dataset.
  
  ![image](https://github.com/user-attachments/assets/44ae865a-113b-43e5-b0e2-aaf49ccce14e)
  
Click on Sink and then “+” button, then search Azure Data Lake Storage Gen2, after it select “Delimited Text” because we are trying to save the data in same format. Click on Continue.

  ![image](https://github.com/user-attachments/assets/5ca149fc-415d-4ea7-a728-7dfc869822a0)
  
Name the Sink properties like AthletesSink, for first time we have to  link the destination then after we use the same destination to save all our data. So, click on +New, 
After moving t next page select Azure subscription and Storage Account Name.
Click on Create. After that select the path where we want to save our raw data. Give the name of the file, And select Import Schema “None”. click on Ok
  
  ![image](https://github.com/user-attachments/assets/cd4984f5-f505-42a0-8a99-266030f0ea50)
  
Click on Validate to verify the everythings setup.
  
  ![image](https://github.com/user-attachments/assets/ee779074-e542-4b37-a71b-97724a5e7a83)
  
The click on Debug, then after it is shoding with green tick mark, that means it is validated and the data is save to defined location, so we go back to Data storage account->Container and we will see our data.
  
  ![image](https://github.com/user-attachments/assets/ffda0ad5-c274-4116-bd77-3876ba576aa5)
  ![image](https://github.com/user-attachments/assets/eacc289a-d6ae-4d47-8114-de67a45379c2)

Same wise we do for others. Source step is same but in sink step we do not create new Sink location we directly select the created one and click on Create.
  
  ![image](https://github.com/user-attachments/assets/ffbe0a5d-1b1b-4ec5-b9dc-e12da8aad36b)

4. **Drag and Drop Operation**: Drag the “Copy data” activity and drop it in the designated area.

   Raw data links:
   - Athletes.csv : https://raw.githubusercontent.com/tanya88099/OlympicData/main/Dataset/Athletes.csv
   - Coaches.csv : https://raw.githubusercontent.com/tanya88099/OlympicData/main/Dataset/Coaches.csv
   - EntriesGender.csv : https://raw.githubusercontent.com/tanya88099/OlympicData/main/Dataset/EntriesGender.csv
   - Medals.csv : https://raw.githubusercontent.com/tanya88099/OlympicData/main/Dataset/Medals.csv
   - Teams.csv : https://raw.githubusercontent.com/tanya88099/OlympicData/main/Dataset/Teams.csv
  
After adding all the source data , make a joint like the below figure only you have to do is drag and drop. validate and Debug the everything and click on publish All.
  
  ![image](https://github.com/user-attachments/assets/3f953d9f-d37c-4808-a06f-0a6fc61a289c)
  ![image](https://github.com/user-attachments/assets/b7042f70-daf7-4a5a-8de6-1ccd446eb561)


### Setting Up Databricks

1. **Search for Databricks**: Search for Databricks in the search bar and create a new Databricks service.
  
2. **Configure Databricks**:
   - Use the resource group and free trial subscription.
   - Select your location and give a Databricks name.
   - After deployment, click on "Launch Workspace".
     
     ![image](https://github.com/user-attachments/assets/d21ff9a8-596a-4149-928e-0fb3bde158bf)
     ![image](https://github.com/user-attachments/assets/39a80d46-3192-4259-ac62-86890b2bc453)

3. **Create Compute Cluster**:
   - Go to the "Compute" tab and create a new compute cluster.
   - Select policy: Unrestricted.
   - Access mode: Single node.
   - Performance: 12.2LTS (includes Apache Spark 3.3.2, Scala 2.12).
   - Node type: Standard_DS3_v2 (14GB, 4 Core).
   - Click "Create".
     
     ![image](https://github.com/user-attachments/assets/9c028075-3379-45eb-bab0-7e4ab01af90f)
     
   - Click on New -> Notebook.
     
     ![image](https://github.com/user-attachments/assets/4178e8d9-d673-47da-b36d-1925039dd48b)
     
To make a connection so that we can connect to the data lake storage gen 2 to databricks so that we can access the raw data and transform it and save it to transform folder . for that we need to create App Registrations.
   
### Connecting Databricks to Data Lake Gen 2

1. **Create App Registration**:
   - Name it "app01" and create it.
   - Copy the client ID and tenant ID for future use.
   - Go to the "Certificate & secrets" under the Manage tab.
   - Click on "New client secret", give it any name, and click "Add". Copy the secret key value.

     ![image](https://github.com/user-attachments/assets/ccf39328-8562-4868-8e98-47fbacdb242f)
     ![image](https://github.com/user-attachments/assets/d055157d-f34c-4926-a066-e075d9a51c2d)
     
     Well this is a not right way to do but now for understanding we just take a copy of it and we will use it further.
     Then we come back to our DataBricks Notebook: Here we use some code to make  connections.
2. Back to Notebook and start coding to transform the raw data and save it to transformed-data folder.
   - **Imports necessary libraries:** Imports col from pyspark.sql.functions and data types from pyspark.sql.types for potential use in later DataFrame operations.
    ```python
    from pyspark.sql.functions import col
    from pyspark.sql.types import IntegerType, DoubleType, BooleanType, DateType
    ```
     - **Defines configuration:** Creates a dictionary configs to store authentication details for accessing the ABFS container using OAuth.
    ```python
    configs = {"fs.azure.account.auth.type": "OAuth",
    "fs.azure.account.oauth.provider.type": "org.apache.hadoop.fs.azurebfs.oauth2.ClientCredsTokenProvider",
    "fs.azure.account.oauth2.client.id": "", #put client ID here
    "fs.azure.account.oauth2.client.secret": '', # put secret Value here
    "fs.azure.account.oauth2.client.endpoint": "https://login.microsoftonline.com/tanent_id/oauth2/token"} # put tanent_id here
    ```
    -**Mounts the container:** Uses dbutils.fs.mount to mount the specified ABFS container to a specified mount point within the Databricks workspace.
    ```python
    dbutils.fs.mount(
    source = "abfss://tokyodecontainer@tokyodesatanya.dfs.core.windows.net", # contrainer@storageacc
    mount_point = "/mnt/tokyoolymic",
    extra_configs = configs)
    ```
    The above code establishes a connection to your Azure Blob Storage and makes its contents accessible within your Databricks environment for further data processing and analysis.
    -**Checking Directory Contents:**
       -%fs: This is a magic command specific to Databricks notebooks. It allows you to interact with the Databricks File System (DBFS).
       -ls "/mnt/tokyoolymic": This command lists the contents of the directory /mnt/tokyoolymic within DBFS. This directory was likely mounted earlier using the code you saw before.
    ```python
    %fs
    ls "/mnt/tokyoolymic"
    ```
    ![image](https://github.com/user-attachments/assets/4a51fe36-8f2d-4fe0-9539-e9fd5d7987b4)
   
   -Reading Data from Mounted Storage:
    athletes = spark.read.format("csv").option("header","true").option("inferSchema","true").load("/mnt/tokyoolymic/raw-data/athletes.csv"): This line reads data from a CSV file using Spark SQL. Let's break down what it does:
    athletes =: Assigns the result of the spark.read operation to a variable named athletes.
    spark.read: This initiates a Spark DataFrame reader.
    .format("csv"): Specifies that the data format is CSV.
    .option("header","true"): Indicates that the CSV file has a header row containing column names.
    .option("inferSchema","true"): Instructs Spark to automatically infer the data types of each column based on the data it reads.
    .load("/mnt/tokyoolymic/raw-data/athletes.csv"): Specifies the path to the CSV file you want to read. The path indicates the file is located within the /raw-data subdirectory of the mounted /mnt/tokyoolymic directory.
    Overall, this code snippet checks the contents of the mounted directory to verify the presence of the athletes.csv file and then reads that file into a Spark DataFrame named athletes for further processing.
   ```python
    athletes = spark.read.format("csv").option("header","true").option("inferSchema","true").load("/mnt/tokyoolymic/raw-data/athletes.csv")
    coaches = spark.read.format("csv").option("header","true").option("inferSchema","true").load("/mnt/tokyoolymic/raw-data/coaches.csv")
    entriesgender = spark.read.format("csv").option("header","true").option("inferSchema","true").load("/mnt/tokyoolymic/raw-data/entriesgender.csv")
    medals = spark.read.format("csv").option("header","true").option("inferSchema","true").load("/mnt/tokyoolymic/raw-data/medals.csv")
    teams = spark.read.format("csv").option("header","true").option("inferSchema","true").load("/mnt/tokyoolymic/raw-data/teams.csv")
    ```
   ```python
    athletes.show()
   ```
   ![image](https://github.com/user-attachments/assets/42f8245a-a845-46e6-bbdc-f37b984add5b)
     ```python
    athletes.printSchema()
   ```
    ![image](https://github.com/user-attachments/assets/b5d346e3-7767-41d1-af31-6e155e603b52)
     ```python
    coaches.show()
   ```
    ![image](https://github.com/user-attachments/assets/647d4793-af05-4790-beb9-52e5d684c054)

### Data Analysis with Azure Synapse Analytics

1. Set up an Azure Synapse workspace.
2. Load the transformed data from Data Lake Gen 2 into Synapse.
3. Perform data analysis using SQL and other available tools.

### Visualization with Power BI/Looker Studio/Tableau

1. Connect to the analyzed data in Synapse or Data Lake Gen 2.
2. Create interactive dashboards and reports to visualize key insights from the Olympic dataset.

## Conclusion

This end-to-end project demonstrates the power and flexibility of Microsoft Azure services for data engineering and analytics tasks. By leveraging Azure Data Factory, Data Lake Gen 2, Synapse Analytics, and Databricks, we can efficiently ingest, transform, analyze, and visualize complex datasets to uncover valuable insights.

For more details and to download the dataset, visit the [OlympicData GitHub repository](https://github.com/tanya88099/OlympicData/tree/main/Dataset).
