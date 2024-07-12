# Personalized Product Recommendation System


# Table of Contents

1. [Overview](#overview)
2. [Architecture](#architecture)
3. [Deployment](#deployment)
4. [Notebooks](#notebooks)
   1. [Data Preparation](#data-preparation)
   2. [Personalization with Amazon Personalize](#personalization-with-amazon-personalize)
   3. [Email Generation with Amazon Bedrock](#email-generation-with-amazon-bedrock)
   4. [Resource Cleanup](#resource-cleanup)

# Overview


The primary intent for this solution is to deliver a personalized and engaging experience to customers, ultimately leading to increased customer satisfaction, loyalty, and revenue growth for the business. Customers expect seamless and tailored experiences that directly address their unique preferences and needs and achieving that level of personalization can be a challenge for businesses with large customer bases and catalogs.

The workflow begins by ingesting data from Amazon S3, including product catalogs, customer information, and user interactions such as reviews on products. This data is then processed to extract relevant information about products and users and stored back to Amazon S3. Sentiment analysis using Amazon Comprehend is performed on user interactions, particularly product reviews, to gauge customers' preferences, opinions, and sentiments towards specific products or features. The extracted product and user data, along with the interaction data, are stored in Amazon DynamoDB for efficient data management and retrieval.

Amazon Personalize, a machine learning service, plays a crucial role in generating personalized product recommendations for each customer. It leverages the stored data, including user preferences and entiment analysis results, to create tailored recommendations for each user. These personalized recommendations are then integrated into email templates using Amazon Bedrock Claude which ensures that each customer receives a dynamic and personalized email content tailored to their specific interests and needs.

By delivering personalized recommendations and tailored communications, customers feel valued and understood, leading to increased satisfaction and loyalty. This personalized approach sets the business apart from competitors and creates a memorable and positive brand experience. Moreover, personalization has been proven to significantly impact conversion rates. By presenting customers with products and offers that align with their preferences, the likelihood of making a purchase increases, driving revenue growth for the business.


### Architecture

<img width="877" alt="Screenshot 2024-07-09 at 11 01 09 AM" src="https://github.com/anyakhatri/Personalize-Recommendations-and-Emails-with-Bedrock/assets/88737540/5725b3a3-e227-43f5-a0d1-8bc38e806339">


## Cost
You are responsible for the cost of the AWS services used while running this Guidance. As of  , the cost for running this Guidance with the default settings in the US West (Orgeon) is approximately $<n.nn> per month for processing (  records ).



## Sample Cost Table
When estimating the cost for this architecture, we are working with 1500 customers and generating 5 recommendations per user.

| AWS Service | Dimension | Cost [USD] |
| --- | --- | --- |
| Amazon Personalize Training Hours | 300 training hours x $0.24 USD | $72.00 |
| Amazon Personalize Real Time Inferencing | 24 hours x 30 days x 9 TPS = 6480<br>6480 x $0.20 USD | $1296.00 |
| Amazon Comprehend | 1500 active dataset rows x 6 units per request<br>90,000 x 0.0005 | $45.00 |
| Amazon DynamoDB | Write Cost = $150.04<br>$150.04 + $26.14 | $176.18 |
| Amazon SNS | Monthly Cost + 1500 x 0.00002 USD | |
| Amazon S3 Storage | 1 GB x $0.023 USD | $2.30 |
| Amazon Sagemaker | 300 training hours x $2.17 USD | $651.00 |
| Total | |  |


# Prerequisites

Before running the notebooks, ensure that you have the following:

1. AWS account with appropriate permissions
2. Jupyter Notebook environment set up
3. Python and necessary libraries installed (e.g., boto3, pandas)


## Deployment Steps

1. Deploy the CloudFormation Stack:
   - Use the AWS Management Console, AWS CLI, or AWS CloudFormation APIs to create a new CloudFormation stack based on the template created in step 1
   - Provide the required parameters, such as the S3 bucket name, notebook instance configuration, and any other necessary inputs.
2. Clone the Repository:
   - Clone the repository containing the notebooks and necessary code for the workflow.
   - This repository should include the data preprocessing, sentiment analysis, personalization, and email template integration scripts.
  
3. Upload amazon.csv to the S3 Bucket
   - Navigate to the S3 bucket created from the CloudFormation Stack and upload amazon.csv to the bucket.

4. Open the SageMaker Notebook Instance:
   - Launch the SageMaker notebook instance provisioned by the CloudFormation stack.
   - Upload the 4 notebooks in the same instance

5. Run the Notebooks in Order

   (1) Dataset filtering
   
   (2) Personalization
   
   (3) Bedrock Implementation
   
   (4) Cleanup

## Deployment Validation
# Running the Guidance

### 1. Data Preparation

This notebook takes an Amazon product dataset (amazon.csv) and filters it to extract relevant product and user data. It then writes the data back to DynamoDB and creates an interaction dataset. Finally, it saves these files to an Amazon S3 bucket.

Explanation:

- ***DynamoDB***: A fully managed NoSQL database service provided by AWS. It is used to store the product and user data for efficient retrieval.
- ***Amazon S3***: A highly scalable and durable object storage service. It is used to store the interaction dataset for later use.

Steps:
1. Install and import necessary libraries (e.g., boto3, pandas)
2. Read the amazon.csv dataset
3. Filter the dataset to extract product and user data
4. Write the product and user data to DynamoDB
5. Create an interaction dataset
6. Save the datasets to an Amazon S3 bucket

### 2. Personalization with Amazon Personalize

This notebook creates a dataset group in Amazon Personalize and imports the three files (product data, user data, and interaction data) created in the previous notebook. It defines the schema, chooses a user personalization recipe (e.g., USER_PERSONALIZATION), and generates five personalized recommendations for each user.

Explanation:

- ***Amazon Personalize***: A machine learning service that enables the creation of personalized recommendations based on user data and interactions.
- ***User Personalization***: This recipe uses collaborative filtering, which analyzes patterns of user behavior and interactions to generate personalized recommendations for each user.

Steps:

1. Install and import necessary libraries (e.g., boto3, pandas)
2. Create a dataset group in Amazon Personalize
3. Import the product data, user data, and interaction data files into the dataset group
4. Define the schema for the dataset group
5. Choose the USER_PERSONALIZATION recipe
6. Create a solution and start the model training process
7. Deploy the solution for real-time recommendations
8. Generate five personalized recommendations for each user

  
### 3. Email Generation with Amazon Bedrock
This notebook generates an email template using Amazon Bedrock, populating it with personalized recommendations and the user's name. It explains how AWS Bedrock works in this case and how it simplifies the process of generating and sending personalized emails.

Explanation:

- ***Amazon Bedrock***: An open-source project that provides a comprehensive framework for building and deploying modern applications on AWS.
- ***Email Generation***: AWS Bedrock can be used to generate personalized emails by leveraging Claude for template and data manipulation capabilities.

Steps:

1. Install and import necessary libraries (e.g., AWS Bedrock, Jinja2)
2. Populate the template with personalized recommendations and user data
3. Generate the email content for each user



### 4. Resource Cleanup (#resource-cleanup)
This notebook provides instructions on how to clean up the resources created during the previous steps, such as deleting the DynamoDB tables, Amazon S3 buckets, and Amazon Personalize resources.

Steps:

1. Delete the DynamoDB tables used for storing product and user data
2. Delete the Amazon S3 bucket used for storing the interaction dataset
3. Delete the Amazon Personalize dataset group, solution, and other related resources

