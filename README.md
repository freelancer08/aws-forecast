# Zero to Hero: Amazon Forecast

This tutorial will provide you a quick introduction on how Machine Learning would be able to help businesses, and by leveraging cloud platforms such as Amazon Forecast and Amazon Sagemaker will help accelerate development and realise business value, faster (time-to-market).

To give you a bit more background, Amazon Forecast is a fully managed service that uses machine learning to deliver highly accurate forecasts. It uses a variety of algorithms to analyze data and generate accurate predictions. It can be used to forecast customer demand, inventory levels, financial performance, and other business metrics. It is easy to set up and requires no machine learning experience. With Amazon Forecast, businesses can make more informed decisions, reduce costs, and improve customer experience.

<img title="AWS Forecast" alt="Seeing the future" src="/images/AWSForecast.jpeg">

To bring more flavour and appreciation on this topic, we will be using Forecast to predict the Sales on a particular shop/retail store.

## Business Background:
- Client owns a shop/retail store in the US (as we will be leveraging US holidays) and currently projecting sales using primitive rolling 52 week approach.
  - Link on this approach https://www.lawinsider.com/dictionary/52-week-rolling-forecast
- Client is trying to project a more realistic forecast

## Solution:
- We'll use Machine Learning algorithm leveraging Amazon Forecast to get a more accurate sales number, providing better business insights and can be used for gamification such as "Sales Competition" within the company.

## Solution Overview:

The following provides an overview of a high-level data platform architecture.

<img title="High-level Data Architecture" alt="Seeing the future" src="/images/aws-forecast-architecture-HighLevelArchitecture.drawio.png">

**Data platform** functions are the operations that are performed on data in order to make it available for use. This includes data ingestion, transformation, processing, analysis and visualization.

**Data Ingestion** is the process of collecting data from various sources and loading it into a data platform. This can be done manually or automatically, depending on the type of data and the platform. Data ingestion can involve extracting data from databases, files, web services, or other sources.

**Data Transformation** is the process of transforming data from one format to another. This is often done to make the data more useful or to make it easier to analyze. Data transformation can involve cleaning, filtering, normalizing, and transforming data from one format to another.

**Data Processing** is the process of transforming data into a format that can be used for analysis. This can involve aggregating data, performing calculations, or applying algorithms to the data.

**Data Analysis** is the process of extracting meaningful insights from data. This can involve using statistical methods, machine learning algorithms, or other methods to analyze the data.

**Data Visualization** is the process of creating visual representations of data. This can involve creating charts, graphs, maps, or other visualizations to help make the data easier to understand.


## Solution Approach and Components:

We will be leveraging AWS Cloud to address the business requirements.  The following architecture will provide you an overview on what are the different components within AWS Cloud that we will leverage for the end-to-end solution.

The scope of this tutorial will be focused on AWS Forecast <span style="color:green">*(highlighted in green)*</span> and provide you a better understanding on how these AWS Cloud Native services can be easily provisioned helping the business to realise the value of their data without building a complex infrastructure and platform.

<img title="AWS Forecast Architecture Overview and Tutorial Scope" alt="Seeing the future" src="/images/aws-forecast-architecture-AWS-Forecast-Tutorial.drawio.png">

The following are some of the key components I want to highlight and hopefully will give you a better understanding on the approach and its functions:

**AWS Managed Workflows for Apache Airflow (MWAA)** is a fully managed workflow orchestration service that makes it easy to set up, operate, and scale Apache Airflow on AWS. MWAA allows you to quickly create and manage data pipelines that automate the movement and transformation of data. MWAA also provides an intuitive web-based UI for creating and managing workflows, and it supports a variety of programming languages, including Python, Java, and JavaScript.

**AWS Glue** is a fully managed extract, transform, and load (ETL) service that makes it easy for customers to prepare and load their data for analytics. AWS Glue also provides a data catalog that stores metadata about data sources, tables, and their schemas, making it easier to discover and share data across various teams.

**AWS Athena** is an interactive query service that makes it easy to analyze data in Amazon S3 using standard SQL. Athena is serverless, so there is no infrastructure to manage, and you pay only for the queries that you run. Athena is integrated with AWS Glue Data Catalog, allowing you to create a unified view of your data stored in S3. Athena is highly scalable, allowing you to run queries on petabytes of data in seconds.

**AWS SageMaker** is a fully managed service that enables developers and data scientists to quickly and easily build, train, and deploy machine learning models at any scale. It provides a suite of tools and services that make it easy to build, train, and deploy machine learning models in the cloud.  SageMaker also provides a range of tools for monitoring and managing machine learning models, such as model performance metrics, model versioning, and model deployment.

## Knowledge Pre-requisites for the AWS Forecast Tutorial: 
- AWS Cloud, S3, and Sagemaker Services
- Good understanding on Jupyter Notebook
- Basic Python programming background

## AWS Forecast Tutorial Lab and Sagemaker Studio Setup

We will be mainly using Sagemaker for this Lab.  Do ensure you've your AWS Account provisioned.  This will also require approximately less than US$5 if you're not using any credits or freetier services.

1.  Open **AWS Console** and on the upper right area, switch to the **AWS Region** of your choice.
   <img title="AWS Select Region" alt="AWS Select Region" src="/images/aws-region-selection.png">

2. Under services, search for **Sagemaker**, and choose **Amazon Sagemaker**.
  <img title="AWS Search Sagemaker" alt="AWS Search Sagemaker" src="/images/aws-search-sagemaker.png">

1.  On the left side of the console, under Admin Confiugrations, choose **Domains** then click **Create Domain**
   <img title="AWS Create Sagemaker Domain" alt="AWS Create Sagemaker Domain" src="/images/aws-select-create-sagemaker-domain.png">

2.  Choose the **Quick Setup** and click **Set up**.
   <img title="AWS Quick Setup Sagemaker Domain" alt="AWS Quick Setup Sagemaker Domain" src="/images/aws-quick-setup-sagemaker-domain.png">

3.  In Studio, you can now select the newly created domain with defaul user profile.  Click **Open Studio**
   <img title="AWS Open Default Sagamaker Studio User" alt="AWS Open Default Sagamaker Studio User" src="/images/aws-open-studio-default-sagamaker-user.png">

4.  This would take few minutes.
   <img title="AWS Creating Amazon Sagemaker Studio" alt="AWS Creating Amazon Sagemaker Studio" src="/images/aws-creating-amazon-sagemaker-studio-jupyterserver.png">

5.  Once **Sagemaker** studio IDE is ready, open **File -> New -> Terminal**.
   <img title="AWS Open Sagemaker Studio Terminal" alt="AWS Open Sagemaker Studio Terminal" src="/images/aws-open-terminal-sagemaker-studio.png">

6.  Run the following command on the terminal:
  ```
  git clone https://github.com/freelancer08/aws-forecast.git
  ```
   <img title="AWS Git Clone Freelancer08 AWS Forecast" alt="AWS Git Clone Freelancer08 AWS Forecast" src="/images/aws-git-clone-freelancer08-aws-forecast.png">
  
7.  Click the **Folder Icon** on the left (under the Home icon), and navitage to **aws-forecast/** folder, then open **zero-to-hero-aws-forecast.ipynb** notebook to continue the tutorial using **Jupyter Notebook**. 
   <img title="AWS Open Zero to Hero AWS Forecast Notebook Folder" alt="AWS Open Zero to Hero AWS Forecast Notebook Folder" src="/images/aws-open-zero-to-hero-aws-forecast-notebook-folder.png">

8.  Select the image **Data Science 3.0**, kernel **Python 3**, with instance type **ml.t3.medium** with no start-up script.
   <img title="AWS Select Data Science 3.0 Python 3 and ML T3 Instance" alt="AWS Select Data Science 3.0 Python 3 and ML T3 Instance" src="/images/aws-select-datascience3-python3-ml-t3.png">
9.  Continue the tutorial using **Zero to Hero: Amazon Forecast** Jupyter notebook.
   <img title="AWS Zero to Hero Amazon Forecast Notebook Tutorial" alt="AAWS Zero to Hero Amazon Forecast Notebook Tutorial" src="/images/aws-zero-to-hero-amazon-forecast-notebook-tutorial.png">


## Conclusion:
By now, you should have a good understanding of data platform architecture, AWS Forecast and different AWS Cloud native services that can be leveraged to provide ML driven data insights with speed and scale.

## Next:
I will be creating other blogs on how similar solution can be done on different cloud and on-premises system to give you a view on the differences and strengths of each solution, especially on how these solution will address your client's business requirements.