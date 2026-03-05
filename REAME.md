
## Architecture Overview And High Level Design

## Architecture

This repository demonstrates setup process of an application that will use an agent on Amazon Bedrock

![Diagram](images/diagram.png)

## The solution consists of:

AWS S3 bucket which will be used to store the domain data that the Agent will later use to answer domain specifc questions

Amazon Bedrock Knowledge Base with S3 Data Source, S3 Vector Database, Titan Embedding Model

AWS Lambda function which serves as a backend API for the AI agent

Amazon Bedrock Agent and Action Group

EC2 Instance to run Streamlit UI


## High Level Design.

## Overview
In this project, we will set up an Amazon Bedrock agent with an action group that dynamically creates an investment company portfolio based on specific parameters. The agent also has Q&A capabilities for Federal Open Market Committee (FOMC) reports, leveraging a Streamlit framework for the user interface. 

This README will walk you through the step-by-step process to set up the Amazon Bedrock GenAI agent manually using the AWS Console.

## Setup

### Step 1: Creating S3 Buckets
- Please make sure that you are in the **us-west-2** region. If another region is required, you will need to update the region variable `theRegion` in the `invoke_agent.py` file code. 
- **Domain Data Bucket**: Create an S3 bucket to store the domain data. For example, call the S3 bucket `knowledgebase-bedrock-agent-{alias}`. We will use the default settings.

Give {alias} in bucket name as some unique text

Once bucket create successfully. Upload the pdf files from S3-data directory in this repository to S3 bucket.
These files are the Federal Open Market Committee documents describing monetary policy decisions made at the Federal Reserved board meetings. The documents include discussions of economic conditions, policy directives to the Federal Reserve Bank of New York for open market operations, and votes on the federal funds rate.

### Step 2: Knowledge Base Setup in Bedrock Agent

Please make sure you are not logged in as root user to create KB. If yes, create a admin user in IAM and then proceed with below steps to create KB.

Open Amazon Bedrock and Navigate to Knowledge Bases under Build

![KB](images/KB.png)

selecting the orange button **Create knowledge base** with dropdown option **Knowledge Base with Vector Store**

![CreateKB](images/Create-KB.png)

You can use the default name, or enter in your own. Then, select **Next** at the bottom right of the screen keeping all default values as it is

Configure S3 database as Data Source by providing S3 Uri as S3 bucket created to store pdf data. Rest Keep Default and press Next

For the embedding model, choose **Amazon: Titan Embeddings G1 - Text**. Choose Vector Store type as **Amazon S3 Vectors** and scroll down to select **Next**.

![Embd](images/Embeddings-model.png)

- On the next screen, review your work, then select **Create knowledge base**
(Creating the knowledge base may take a few minutes. Please wait for it to finish before going to the next step.)

Once your Knowledge Base is created successfully. you can that listed in Konwledge bases as below

 ![Kb-done](images/KB-done.png)
 






