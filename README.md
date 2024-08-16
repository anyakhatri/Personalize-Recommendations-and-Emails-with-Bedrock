<h1 align="center">Guidance-fore-Personalized-Recommendation-Notifications-on-AWS</h1>


## Table of Contents

- [Overview](#overview)
- [Architecture](#architecture)
- [Cost](#cost)
  - [Sample Cost Table](#sample-cost-table)
- [Prerequisites](#prerequisites)
- [Deployment Steps](#deployment-steps)
- [Deployment Validation](#deployment-validation)
- [Running the Guidance](#running-the-guidance)
  - [1. Data Preparation](#1-data-preparation)
  - [2. Personalization with Amazon Personalize](#2-personalization-with-amazon-personalize)
  - [3. Email Generation with Amazon Bedrock](#3-email-generation-with-amazon-bedrock)
  - [4. Resource Cleanup](#4-resource-cleanup)
- [Next Steps](#next-steps)
- [Notices](#notices)
  
## Overview


The primary intent for this solution is to deliver a personalized and engaging experience to customers, ultimately leading to increased customer satisfaction, loyalty, and revenue growth for the business. Customers expect seamless and tailored experiences that directly address their unique preferences and needs and achieving that level of personalization can be a challenge for businesses with large customer bases and catalogs.

The workflow begins by ingesting data from Amazon S3, including product catalogs, customer information, and user interactions such as reviews on products. This data is then processed to extract relevant information about products and users and stored back to Amazon S3. Sentiment analysis using Amazon Comprehend is performed on user interactions, particularly product reviews, to gauge customers' preferences, opinions, and sentiments towards specific products or features. The extracted product and user data, along with the interaction data, are stored in Amazon DynamoDB tables.

Amazon Personalize plays a crucial role in generating personalized product recommendations for each customer. It leverages the stored data, including user preferences and sentiment analysis results, to create tailored recommendations for each user. These personalized recommendations are then integrated into email templates using Amazon Bedrock Claude which ensures that each customer receives personalized email content tailored to their specific interests and needs.

By delivering personalized recommendations and tailored communications, customers feel valued and understood, leading to increased satisfaction and loyalty. This personalized approach sets the business apart from competitors and creates a memorable and positive brand experience. Moreover, personalization has been proven to significantly impact conversion rates. By presenting customers with products and offers that align with their preferences, the likelihood of making a purchase increases, driving revenue growth for the business.


### Architecture

<img width="955" alt="architecture" src="https://github.com/user-attachments/assets/1157c154-d91f-4d42-a085-8a577b07f14a">



### Cost
You are responsible for the cost of the AWS services used while running this Guidance. As of 7/15/24, the cost for running this Guidance with the default settings in the US West (Oregon) is approximately $74.53 based on the following assumptions.


### Sample Cost Table
When estimating the cost for this architecture, we are working with 1500 customers and generating 5 recommendations per user.

| AWS Service | Dimension | Cost [USD] |
| --- | --- | --- |
| Amazon Personalize Ingestion, Training and Inference |  (3 x $0.05)+ (3 x 5 hours x $0.24) + (22,500 / 1000 x $0.20)  | $8.25 |
| Amazon Comprehend | (1500 rows x 300 characters)/100 character/unit <br>  4,500 units / 1,000 units x $1.00 | $4.50 |
| Amazon DynamoDB | WRU :1500×24×30=1,080,000 x $1.25 <br> RRU: 1500×24×30=1,080,000 x 0.25 <br> 1 GB×0.25  | $20.76 |
| Amazon S3 Storage | 1 GB x $0.023 USD | $2.30 |
| Amazon Sagemaker | 4 notebooks x $1.935 x 5 hours | $38.72 |
| Total | | $74.52 |


## Prerequisites

Before running the notebooks, ensure that you have the following:

1. AWS account with appropriate permissions


## Deployment Steps



**1. Clone the Repository**
   - Clone the repository with the notebooks and deployment instructions using the command below:
```bash
git clone https://github.com/anyakhatri/Personalize-Recommendations-and-Emails-with-Bedrock.git
```


**2. Deploy the CloudFormation Stack:**
   - Use the AWS Console to navigate to the CloudFormation console. [CloudFormation template](https://github.com/anyakhatri/Personalize-Recommendations-and-Emails-with-Bedrock/blob/main/deployment/deployment.yaml), also found in deployment/deployment.yaml and follow the steps demonstrated below.
     


https://github.com/user-attachments/assets/baeece97-e46e-49df-b141-5c808e519fe5




**3. Upload amazon.csv to the S3 Bucket**
   - Navigate to the S3 bucket created from the CloudFormation Stack and upload deployment/amazon.csv to the bucket.
  
  <img width="1233" alt="Screenshot 2024-08-05 at 2 07 20 PM" src="https://github.com/user-attachments/assets/b563dda7-fdc9-4fc1-b09f-021bf7a2e571">




**4. Choose Bedrock Model**
  - Before you can use any Bedrock Models, you need to request model access through the AWS Console in a region where Bedrock is available. Follow documentation found [here](https://docs.aws.amazon.com/bedrock/latest/userguide/model-access.html).  Activate "Claude 3 Sonnet". Then, click "Save changes".

<img width="523" alt="Screenshot 2024-07-16 at 12 33 26 PM" src="https://github.com/user-attachments/assets/51e833f2-959a-4de1-83cf-9ed3ae3fcea3">


**5. Open the SageMaker Notebook Instance:**
- In the AWS Management Console, search for the "SageMaker" service
- Once in the SageMaker service, navigate to Notebooks under Application and IDE's.
- Click on the Notebook Instance, recommendationsystem, which was created by out CloudFormation Template
- In the Notebook Instance details page, click on the "Open Jupyter" or "Open JupyterLab" button to launch the Jupyter Notebook environment.
- Follow the guidance below to upload all 4 notebooks to the instance.
  
     

https://github.com/user-attachments/assets/48c25615-e538-4886-9b3d-28a2dadbc8ad








## Deployment Validation

1. Open the AWS CloudFormation console and navigate to the stack you just created. Verify the status of the stack by checking the "Status" column. If the deployment is successful, the status should be "CREATE_COMPLETE".

<img width="1228" alt="Screenshot 2024-07-16 at 9 44 40 AM" src="https://github.com/user-attachments/assets/f7847810-2367-435b-b537-f5968bbc0dad">

2. Verify the creation of the following resources:
   - Amazon S3 Bucket: Open the Amazon S3 console and check if the bucket with the name you provided in the BucketName parameter is created
   
  ```bash
   aws s3 ls s3://personalizeproductreviewdata
 ```
   - IAM Roles: Open the IAM console and check if the roles SageMakerIamRole and PersonalizeIamRole are created.
   - Amazon SageMaker Notebook Instance: Open the Amazon SageMaker console and check if the notebook instance with the name you provided in the NotebookName parameter is created and has the status "InService".
  
     <img width="1132" alt="Screenshot 2024-07-16 at 9 45 23 AM" src="https://github.com/user-attachments/assets/f0d09671-5222-48c0-b11c-6c070d368796">


If all the above steps are successful, it indicates that the deployment of the CloudFormation template is successful, and the required resources are created correctly.

## Running the Guidance

   
**Runnng the notebooks:**
  - Open the first notebook, **datasetfiltering(1).ipynb**.
  - Once the notebook is open, you will see a series of cells containing code or text.
  - To run a specific code cell, first, click on the cell you want to execute. You'll notice that the cell's border becomes green, indicating that it's selected.
  - Once you've selected the cell you want to run, click the "Run" button in the toolbar at the top of the notebook. It looks like a "Play" icon.
  - When you run a cell, you'll see a * indicator in the bracket to the left of the cell. This means the cell is currently running. Once the cell has finished executing, the * will change to a sequential number, indicating the order in which the cells were run.

<img width="1187" alt="Screenshot 2024-07-26 at 9 38 39 AM" src="https://github.com/user-attachments/assets/be464b34-1e0a-441d-9e0e-a17e2e4ffa37">

Repeat this process for all notebooks in the following order following datasetfiltering(1).ipynb:

**(2) Personalization**

**(3) Bedrock Implementation**

**(4) Cleanup**


## Here is a deeper look into each notebook:

### 1. Data Preparation

This notebook takes an Amazon product dataset (amazon.csv) and filters it to extract relevant product and user data. It then writes the data back to DynamoDB and creates an interaction dataset. Finally, it saves these files to an Amazon S3 bucket.

Explanation:

- ***DynamoDB***: A fully managed NoSQL database service known for its low-latency performance and scalability. It is used to store the product and user data for efficient retrieval.
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

- ***Amazon Bedrock***: Amazon Bedrock is a fully managed service that offers a choice of high-performing foundation models (FMs
- ***Email Generation***: Amazon Bedrock can be used to generate personalized emails by leveraging Claude for template and data manipulation capabilities.

Steps:

1. Install and import necessary libraries (e.g., AWS Bedrock)
2. Populate the template with personalized recommendations and user data
3. Generate the email content for each user



### 4. Resource Cleanup 

Run the resource notebook cleanup(4) to clean up all associated resources included in the Jupyter notebooks. To delete the stack, run the following command in the AWS CLI

```bash
aws cloudformation delete-stack --stack-name <YOUR-STACK-NAME>
```


## Next Steps

Here are some suggestions next steps customers can take with this guidance:

Data Source: The current implementation uses a sample Amazon product dataset. Customers can replace this with their own product catalog, customer data, and interaction data to generate personalized recommendations tailored to their business and customer base.

Personalization Recipe: The Guidance currently uses the USER_PERSONALIZATION recipe, but customers can explore other available recipes in Amazon Personalize depending on their use case and data characteristics.

Email Customization: The Guidance provides a basic email template using Amazon Bedrock. Customers can enhance the email template design, content, and personalization features to align with their branding and marketing strategies. Additionally, they can integrate the email generation process with their existing email marketing systems or communication channels.

Scalability: The Guidance is designed to handle a specific number of customers and interactions. Customers can scale the solution by adjusting the AWS resource configurations (e.g., Amazon DynamoDB capacity, Amazon Personalize instance types) to accommodate larger datasets and higher traffic volumes.


## Notices

_Customers are responsible for making their own independent assessment of the information in this Guidance. This Guidance: (a) is for informational purposes only, (b) represents AWS current product offerings and practices, which are subject to change without notice, and (c) does not create any commitments or assurances from AWS and its affiliates, suppliers or licensors. AWS products or services are provided “as is” without warranties, representations, or conditions of any kind, whether express or implied. AWS responsibilities and liabilities to its customers are controlled by AWS agreements, and this Guidance is not part of, nor does it modify, any agreement between AWS and its customers._


## Citations

The dataset is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International (CC BY-NC-SA 4.0) License found [here](https://www.kaggle.com/datasets/karkavelrajaj/amazon-sales-dataset)
