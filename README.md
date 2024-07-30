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

2. **Create Storage Account**: Select "Storage Account" from Popular Azure Services and click "Create".
   ![image](https://github.com/user-attachments/assets/331ee611-1d63-47e2-bec8-c51237379bdb)

3. **Configure Account Details**:
   - Select your subscription.
   - Create a resource group.
   - Provide a unique storage account name.
   - Select performance, redundancy, and region options.
   - Click "Next".
  ![image](https://github.com/user-attachments/assets/1f4a5045-a525-40fe-90ee-7fac1b65e175)

   **Note**: The storage account name must be unique across the region.

4. **Advanced Settings**:
   - Configure the hierarchical namespace, blob storage, security, and Azure Files settings as required.
   - For frequent data access, choose the Hot tier.
   - Enable the “Hierarchical namespace” for directory-like storage organization.
     ![image](https://github.com/user-attachments/assets/a6771a30-bc46-420c-905f-64613ea756ba)
     ![image](https://github.com/user-attachments/assets/7a435553-c920-47ab-ab9a-f4a9fc7a5916)

5. **Networking Settings**:
   - Enable public access from all networks.
   - Configure network routing.
   - Click "Next".
  ![image](https://github.com/user-attachments/assets/f7bf8534-3c40-4ec9-900f-b8e1c9ef2426)


6. **Review and Create**: Proceed through the validation steps to the “Review + create” tab. If the validation passes, click "Create". Deployment will take approximately 2 minutes. After completion, click "Go to resource".
![image](https://github.com/user-attachments/assets/ac1ac162-876f-49a0-8eea-c08d833ad3c1)
![image](https://github.com/user-attachments/assets/7f79503a-eac2-49de-bf56-363d33e9829b)


7. **Creating Containers**:
   - Scroll down the left-side menu and click on "Data Storage -> Container".
   - **Why Containers?**:
     - **Containers (Blob Storage)**: Virtual folders for grouping blobs (files), ideal for storing unstructured data like images, videos, and large files.
     - **File Shares (Azure Files)**: Managed file shares accessible via SMB, suitable for collaborative file access.
     - **Queues (Azure Queue Storage)**: A message queuing service following FIFO order, useful for asynchronous task handling.
     - **Tables (Azure Table Storage)**: A schemaless NoSQL store for large amounts of structured data with flexible schemas.

   Based on our requirements for creating directories to store raw and transformed data, we'll use containers.

8. **Creating Directories**:
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

   ![Pipeline Authoring](https://link_to_image1.png)

2. **Name the Pipeline**: On the right side, it will ask for a pipeline name. Provide a name and click on "Move and transform".
   ![Name Pipeline](https://link_to_image2.png)
   ![image](https://github.com/user-attachments/assets/0769186a-fbcd-45a7-b2b2-2f51d67181eb)


   **Note**: No coding is required here to transform the data; you only need to perform Drag and Drop operations and link the tables.

4. **Drag and Drop Operation**: Drag the “Copy data” activity and drop it in the designated area.

   Raw data links:
   - [Athletes.csv](https://raw.githubusercontent.com/tanya88099/OlympicData/main/Dataset/Athletes.csv)
   - [Coaches.csv](https://raw.githubusercontent.com/tanya88099/OlympicData/main/Dataset/Coaches.csv)
   - [EntriesGender.csv](https://raw.githubusercontent.com/tanya88099/OlympicData/main/Dataset/EntriesGender.csv)
   - [Medals.csv](https://raw.githubusercontent.com/tanya88099/OlympicData/main/Dataset/Medals.csv)
   - [Teams.csv](https://raw.githubusercontent.com/tanya88099/OlympicData/main/Dataset/Teams.csv)
     ![image](https://github.com/user-attachments/assets/188f7f04-3daf-4293-9f91-de64f69ec532)


### Setting Up Databricks

1. **Search for Databricks**: Search for Databricks in the search bar and create a new Databricks service.
  
2. **Configure Databricks**:
   - Use the resource group and free trial subscription.
   - Select your location and give a Databricks name.
   - After deployment, click on "Launch Workspace".
     ![image](https://github.com/user-attachments/assets/08885571-d801-4e4f-8e49-c9726ca689f6)

3. **Create Compute Cluster**:
   - Go to the "Compute" tab and create a new compute cluster.
   - Select policy: Unrestricted.
   - Access mode: Single node.
   - Performance: 12.2LTS (includes Apache Spark 3.3.2, Scala 2.12).
   - Node type: Standard_DS3_v2 (14GB, 4 Core).
   - Click "Create".
     ![image](https://github.com/user-attachments/assets/9c028075-3379-45eb-bab0-7e4ab01af90f)
   
### Connecting Databricks to Data Lake Gen 2

1. **Create App Registration**:
   - Name it "app01" and create it.
   - Copy the client ID and tenant ID for future use.
   - Go to the "Certificate & secrets" under the Manage tab.
   - Click on "New client secret", give it any name, and click "Add". Copy the secret key value.
