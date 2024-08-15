# 💻Automatically apply Terraform and Docker with AWS Codebuild (CI/CD)☁️

Hi! Welcome to my repository containing my AWS Project I've have undertaken as a Cloud Engineer and Cloud architect enthusiast⚡️:

In this repository you will see a description of the project, low and high level architecture, scripting files and information on other key assets that I have used to develop this project as part of my portfolio and progressive development.


## **Project Overview** 

This project demonstrates how create a CodeBuild project that automatically applies your Terraform scripts whenever I commit changes in the GitHub repository. I'll also create a CodeBuild project that automatically builds any Docker image and push it to the Docker Hub repository.

![Low Level Architectural Diagram](https://github.com/user-attachments/assets/f0eb3f39-5be1-4e78-9e27-c0fc83eb2cdd)



- - - 
## **Architecture**

1. **IAM User:** CodeBuild will use User Credentials to authenticate with the AWS environemnt when the Build Project is being created


## **Deployment Steps**

### Create IAM User with Full Access
1. Create an IAM user and grant this user administrative access under policies
2. Ensure to download the User Credentials containing the access key ID and Secret Access Key as AWS will display the users Secret Access Key

### Create and clone a GitHub Repository
1. Create a repository for the Terraform Project and clone the repository
2. Purpose of this is to create a CodeBuild Job that will automaticaly apply the Terraform anytime there is a commit into the GitHub repository
3. For the purspose of this project the files required to create a CodeBuild will be located in the repository titled 'ec2.tf' and 'install_techmax.sh'
4. Clone the repository to your computer using the SSH tab option
5. using the terminal or command prompt change directory to where you want the cloned repository stored and use the command 'git clone' followed by pasting the SSH link into the terminal or command prompt and click enter
6. The Terraform file provided will launch the EC2 instance and install the HTML website on it

### Test the Terraform Script
1. 
