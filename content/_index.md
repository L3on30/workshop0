+++
title = "Workshop 0"
date = 2024
weight = 1
chapter = false
+++

# Build a Serverless Web Application using Generative AI

#### Overview
In this workshop, I will do the process of using **AWS Amplify** to build a **serverless web application** powered by Generative AI, utilizing **Amazon Bedrock** and the **Claude 3 Sonnet** foundation model. The application will feature an HTML-based user interface for ingredient submission and a backend web application that handles requests for AI-generated recipes.

{{% notice warning %}}
Having a free tier or not, if you use **AWS Bedrock**, especially with models like **Claude 3 Sonnet**, may incur additional charges. Please review the [AWS Bedrock pricing](https://aws.amazon.com/bedrock/pricing/) to understand the potential costs before proceeding.
{{% /notice %}}


#### Prerequisites
Before attending this workshop, participants should have:

- **An AWS account**: If you don't already have one, follow the instructions in the **[Setup Your Environment](https://aws.amazon.com/getting-started/guides/setup-environment/)** section.
- **AWS CLI/AWS profile [configured](https://docs.amplify.aws/react/start/account-setup/)** for local development.
- **[Node.js](https://nodejs.org/en/download)** and **[npm](https://www.npmjs.com/)** on your development environment.
- **Familiarity with Git** and a **[GitHub account](https://github.com/)**.

#### Application Architecture
The architecture of this application includes several AWS services, such as **AWS Amplify**,  **AWS Lambda**, **AWS AppSync** and **Amazon Bedrock**. The following diagram provides a visual representation of how these services are connected. Throughout the workshop, participants will learn about each service in detail and find additional resources to help them gain proficiency.

![Image](/images/AWS-workshop0.drawio.png?width=30pc)

#### Main Content
This workshop is structured into the following tasks, which participants must complete in sequence:

1. **[Host a Static Website](1-host-a-static-website/)**: Configure AWS Amplify to host the frontend application with built-in continuous deployment.
2. **[Manage Users](2-manage-users/)**: Set up Amplify Auth and enable access to the Amazon Bedrock foundation model.
3. **[Build a Serverless Backend](3-build-a-serverless-backend/)**: Develop a backend for handling application requests.
4. **[Deploy the backend API](4-deploy-the-backend-api/)**: Define a custom query to connect to Amazon Bedrock
5. **[Build the Frontend](5-build-the-frontend/)**: Set up Amplify Data and connect the frontend application to the backend.
6. **[Clean Up Resources](6-clean-up-resources/)**: Properly clean up and deprovision resources used during the workshop.

By structuring the workshop in this manner, participants will gradually build a fully functional serverless web application while gaining hands-on experience with AWS services and Generative AI.


<!-- need to remove parenthesis for path in Hugo 0.88.1 for Windows-->