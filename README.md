# WordPress_Demo_Application
This Repo is Prepared to present a demo of Wordpress Application to the the representatives of Allianz Technology.

Step-01: Create EKS Cluster using eksctl
         
Prerequisite is to have the AWS CLI installed in your local to configure in which acccount the EKS cluster will be created. Once you have an IAM user and AWS CLI installed in your local, we have to fire a command -:
         
         aws configure
         AWS Access Key ID [None]: (Replace your creds when prompted)
         AWS Secret Access Key [None]: (Replace your creds when prompted)
         Default region name [None]: us-east-1
         Default output format [None]: json

Please note we have to use our own AWS credentials here for the IAM user that you just created. DO NOT USE ROOT CREDENTIALS FOR THE ROOT AWS ACCOUNT.
