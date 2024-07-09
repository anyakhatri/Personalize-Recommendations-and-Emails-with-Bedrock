# Personalized Product Recommendation System


# Table of Contents


1. Overview


### Overview


The primary intent for this solution is to deliver a personalized and engaging experience to customers, ultimately leading to increased customer satisfaction, loyalty, and revenue growth for the business. Customers expect seamless and tailored experiences that directly address their unique preferences and needs and achieving that level of personalization can be a challenge for businesses with large customer bases and catalogs.

The workflow begins by ingesting data from Amazon S3, including product catalogs, customer information, and user interactions such as reviews on products. This data is then processed to extract relevant information about products and users and stored back to Amazon S3. Sentiment analysis using Amazon Comprehend is performed on user interactions, particularly product reviews, to gauge customers' preferences, opinions, and sentiments towards specific products or features. The extracted product and user data, along with the interaction data, are stored in Amazon DynamoDB for efficient data management and retrieval.

Amazon Personalize, a machine learning service, plays a crucial role in generating personalized product recommendations for each customer. It leverages the stored data, including user preferences and entiment analysis results, to create tailored recommendations for each user. These personalized recommendations are then integrated into email templates using Amazon Bedrock Claude which ensures that each customer receives a dynamic and personalized email content tailored to their specific interests and needs.

By delivering personalized recommendations and tailored communications, customers feel valued and understood, leading to increased satisfaction and loyalty. This personalized approach sets the business apart from competitors and creates a memorable and positive brand experience. Moreover, personalization has been proven to significantly impact conversion rates. By presenting customers with products and offers that align with their preferences, the likelihood of making a purchase increases, driving revenue growth for the business.


### Architecture

<img width="859" alt="Screenshot 2024-07-08 at 12 17 41 PM" src="https://github.com/anyakhatri/Personalize-Recommendations-and-Emails-with-Bedrock/assets/88737540/51f56fb2-7923-4710-8b35-541274326e0c">

**Prerequisites**

Before running the notebooks, ensure that you have the following:

1. AWS account with appropriate permissions
2. Jupyter Notebook environment set up
3. Python and necessary libraries installed (e.g., boto3, pandas)


# Architecture

<img width="1125" alt="Screenshot 2024-07-08 at 12 23 56 PM" src="https://github.com/anyakhatri/Personalize-Recommendations-and-Emails-with-Bedrock/assets/88737540/b062479d-db7c-4121-a88f-c88acc30325d">


# Notebooks

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
C6. reate a solution and start the model training process
7. Deploy the solution for real-time recommendations
8. Generate five personalized recommendations for each user

  
### 3. Email Generation with AWS Bedrock
This notebook generates an email template using AWS Bedrock, populating it with personalized recommendations and the user's name. It explains how AWS Bedrock works in this case and how it simplifies the process of generating and sending personalized emails.

Explanation:

- ***AWS Bedrock***: An open-source project that provides a comprehensive framework for building and deploying modern applications on AWS.
- ***Email Generation***: AWS Bedrock can be used to generate personalized emails by leveraging Claude for template and data manipulation capabilities.

Steps:

1. Install and import necessary libraries (e.g., AWS Bedrock, Jinja2)
2. Populate the template with personalized recommendations and user data
3. Generate the email content for each user



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

(1) Dataset filtering
(2) Personalization
(3) Bedrock Implementation
(4) Cleanup
Note: Make sure to update the notebook cells with your AWS credentials and resource names (e.g., S3 bucket names, DynamoDB table names) before running them.
