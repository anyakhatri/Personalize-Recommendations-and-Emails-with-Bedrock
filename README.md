# Personalized Product Recommendation System



### Introduction
In today's digital age, personalization has become a key differentiator for businesses to enhance customer experiences and drive engagement. Recommendation systems play a crucial role in delivering personalized content and product suggestions to users based on their preferences and behaviors.

Amazon Personalize is a machine learning service provided by Amazon Web Services (AWS) that enables developers to build and deploy personalized recommendation engines quickly and easily. It offers a variety of algorithms and recipes tailored for different use cases, such as user personalization (collaborative filtering) and product recommendations (content-based filtering).

Amazon Personalize is an excellent choice for building recommendation systems for several reasons:

- Scalability: It can handle large volumes of data and high traffic loads, making it suitable for applications with millions of users and items.
- Accuracy: Amazon Personalize leverages advanced machine learning techniques to provide accurate and relevant recommendations.
- Ease of Use: It abstracts away the complexities of building and maintaining recommendation models, allowing developers to focus on integrating personalization into their applications.
- Fully Managed: As a fully managed service, Amazon Personalize takes care of provisioning, scaling, and maintaining the underlying infrastructure, reducing operational overhead.
Email Automation with AWS Bedrock and Claude
While Amazon Personalize excels at generating personalized recommendations, delivering those recommendations to users in an engaging and timely manner is equally important. This is where AWS Bedrock and Claude come into play.

AWS Bedrock is an open-source project that provides a comprehensive framework for building and deploying modern applications on AWS. It offers a robust set of tools and best practices for building serverless applications, automating deployments, and managing infrastructure as code. Claude, a component of AWS Bedrock, is a powerful email automation tool that simplifies the process of generating and sending personalized marketing emails. It integrates seamlessly with Amazon Personalize, allowing you to incorporate personalized recommendations into email templates and deliver targeted campaigns to your users.

With Claude, you can:

- Create Responsive Email Templates: Design and develop responsive email templates using modern web technologies like HTML, CSS, and JavaScript.
- Personalize Content: Leverage the integration with Amazon Personalize to populate email templates with personalized recommendations and user-specific content.
- Automate Email Delivery: Automate the process of generating and sending personalized emails to your users, ensuring timely and relevant communication.
- Track and Analyze: Monitor email delivery statistics and user engagement metrics to optimize your campaigns and improve personalization strategies.


By combining the power of Amazon Personalize for generating accurate recommendations and AWS Bedrock with Claude for email automation, you can create a comprehensive personalized recommendation system that delivers a seamless and engaging user experience.

In the following sections, we will explore the step-by-step process of building such a system, including data preparation, model training with Amazon Personalize, email template generation with Claude, and resource management.This repository contains four Jupyter notebooks that demonstrate how to build a personalized product recommendation system. The notebooks cover data preparation, personalization with Amazon Personalize, email generation with AWS Bedrock, and resource cleanup.

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
