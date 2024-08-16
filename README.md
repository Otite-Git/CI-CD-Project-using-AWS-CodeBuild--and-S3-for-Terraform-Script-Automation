# 💻Automatically apply Terraform and Docker with AWS Codebuild (CI/CD)☁️

Hi! Welcome to my repository containing my AWS Project I've have undertaken as a Cloud Engineer and Cloud architect enthusiast⚡️:

In this repository you will see a description of the project, low and high level architecture, scripting files and information on other key assets that I have used to develop this project as part of my portfolio and progressive development.


## **Project Overview** 

This project demonstrates how create a CodeBuild project that automatically applies your Terraform scripts whenever I commit changes in the GitHub repository. I'll also create a CodeBuild project that automatically builds any Docker image and push it to the Docker Hub repository.

![Low Level Architectural Diagram](https://github.com/user-attachments/assets/f0eb3f39-5be1-4e78-9e27-c0fc83eb2cdd)



- - - 
## **Tools used**

1. **IAM User:** CodeBuild will use User Credentials to authenticate with the AWS environemnt when the Build Project is being created
2. **Git:** Used to clone the provided files into the directory
3. **Terraform Script:**  The Terraform file provided will launch the EC2 instance and install the HTML website on it


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

### S3 bucket Creation
1. Create a S3 bucket which will be used to store the Terraform state file as aprt of the script testing
2. Ensure that the S3 bucket given name is unique as the is a requirement for creating an S3 bucket

### Test the Terraform Script
1. Open the repository cloned on your computer. select the Terraform script provided 'ec2.tf' and within the script update the profile name your selected profile name. To create a profile name which will be used, open your Command Line or Terminal and used the command below:
```bash
 aws configure --profile ' specifiy your desired profile name after the command'
 ```
2. Once you select enter you will be asked for your Access Key ID,and Secret Access Key. This can be retrieved from the IAM User file you downloaded as part of creating the IAM USer in the first step above. Lastly you'll be asked for you default region. This can be located in the AWS management console home page
3. Once the profile name is updated in the Terraform script, you will also have to update the 'key_name' with key pair which is one your AWS management console. This can be found in the EC2 service within the key Pair section. Copy and paste that key pair name into the Terraform script replacing the key_name original provided
4. Run the command in VS code below to ensure that we can create the reasources in the file in your AWS account:
```bash
Terraform innit
 ```
This command initialises the file with your AWS environment. This should look like ths:
Provie a screenshot
6. Once initialised the next command to enter is 
```bash
 Terraform apply
```
This command ensures that the resources can be created in the AWS account. This should look like the:
provide screenshot
It will then create the resource in your AWS account 

7. The test requires that the website created on the EC2 instance courtesy of the Terraform script is successfully accessed. Hover over the URL link provided just under outputs, copy and paste the link into your web browser
8. If you can access the website this indicates the Terraform file is successfuly working.
9. Delete the resources using the command below:
```bash
 Terraform destroy
```
It will show you the deletion plan, enter 'yes' and it will delete the resources created in the AWS account. 

10. Once you have tested the Terraform script. Any changes made to the scripted should be pushed to your GitHub repository 

### Shell Script configuration
11. Shell scripts will be created to install Terraform, configure a profile and run the Terraform command.
12. Open the project folder you have been working on as part of this project and create a new folder. All the CI/CD scripts will be contained within this folder 
13. Terraform will have to be installed in the container that CodeBuild will use as part of the project so the first Shell script that will be created is the Shell script which will be used to install Terraform on the container. This will require creating a new file within the new folder you would have create in step 11. For the purposes of this project the Shell script can be found in this repository and it is called 'install-terraform.sh'. Ensure to remain the file name with 'install-terraform.sh'. Copy the script contents within the file and paste it in the new file. Once you have pasted the content inside the file ensure to save it
14. the second Shell script this will be created is the Shell script that will be used to create a named profile in the container. Create another new file within the folder created in step 11. For the purposes of this project the Shell script can be found in this repository and it is called 'configure-named-profile.sh'. Ensure to remain the file name with 'configure-named-profile.sh'. Copy the script contents within the file and paste it in the new file. Once you have pasted the content inside the file ensure to save it
15. The third Shell script that will be created is the script used to create the Terraform command: Terraform init, Terraform apply and Terraform destroy. Create another new file in the folder created above. For the purpose of this project the Shell script can be found in this repository and it is called 'apply-terraform.sh'.  Ensure to remain the file name with 'apply-terraform.sh'. Copy the script contents within the file and paste it in the new file. Once you have pasted the content inside the file ensure to save it
