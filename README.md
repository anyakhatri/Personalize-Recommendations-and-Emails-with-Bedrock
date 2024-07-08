# Personalized Product Recommendation System

This repository contains four Jupyter notebooks that demonstrate how to build a personalized product recommendation system using Amazon Web Services (AWS). The notebooks cover data preparation, personalization with Amazon Personalize, email generation with AWS Bedrock, and resource cleanup.

**Prerequisites**

Before running the notebooks, ensure that you have the following:

1. AWS account with appropriate permissions
2. Jupyter Notebook environment set up
3. Python and necessary libraries installed (e.g., boto3, pandas)

# Notebooks

### 1. Data Preparation

This notebook takes an Amazon product dataset (amazon.csv) and filters it to extract relevant product and user data. It then writes the data back to DynamoDB and creates an interaction dataset. Finally, it saves these files to an Amazon S3 bucket.

Explanation:
DynamoDB: A fully managed NoSQL database service provided by AWS. It is used to store the product and user data for efficient retrieval.
Amazon S3: A highly scalable and durable object storage service. It is used to store the interaction dataset for later use.

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
Amazon Personalize: A machine learning service that enables the creation of personalized recommendations based on user data and interactions.
User Personalization: This recipe uses collaborative filtering, which analyzes patterns of user behavior and interactions to generate personalized recommendations for each user.

Steps:

1. Install and import necessary libraries (e.g., boto3, pandas)
2. Create a dataset group in Amazon Personalize
3. Import the product data, user data, and interaction data files into the dataset group
4. Define the schema for the dataset group
5. Choose the USER_PERSONALIZATION recipe
C6. reate a solution and start the model training process
7. Deploy the solution for real-time recommendations
8. Generate five personalized recommendations for each user

  
### 3. Email Generation with AWS Bedrock
This notebook generates an email template using AWS Bedrock, populating it with personalized recommendations and the user's name. It explains how AWS Bedrock works in this case and how it simplifies the process of generating and sending personalized emails.

Explanation:

AWS Bedrock: An open-source project that provides a comprehensive framework for building and deploying modern applications on AWS.
Email Generation: AWS Bedrock can be used to generate personalized emails by leveraging its templating and data manipulation capabilities.
Steps:

Install and import necessary libraries (e.g., AWS Bedrock, Jinja2)
Define an email template using Jinja2 templating engine
Populate the template with personalized recommendations and user data
Generate the email content for each user
Explain how AWS Bedrock simplifies the email generation process


### 4. Resource Cleanup
This notebook provides instructions on how to clean up the resources created during the previous steps, such as deleting the DynamoDB tables, Amazon S3 buckets, and Amazon Personalize resources.

Steps:

1. Delete the DynamoDB tables used for storing product and user data
2. Delete the Amazon S3 bucket used for storing the interaction dataset
3. Delete the Amazon Personalize dataset group, solution, and other related resources



# Running the Notebooks
To run the notebooks, follow these steps:

Clone the repository or download the notebooks to your local machine.
1. Open the Jupyter Notebook environment.
2. Navigate to the directory containing the notebooks.
3. Run the notebooks in the following order:
Data Preparation
Personalization with Amazon Personalize
Email Generation with AWS Bedrock
Resource Cleanup
Note: Make sure to update the notebook cells with your AWS credentials and resource names (e.g., S3 bucket names, DynamoDB table names) before running them.
