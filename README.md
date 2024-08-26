# 💻Terraform Script automation to install HTML Website with AWS Codebuild and AWS S3 (CI/CD)☁️

Hi! Welcome to my repository containing my AWS Project I've have undertaken as a Cloud Engineer and Cloud architect enthusiast⚡️:

In this repository you will see a description of the project, low and high level architecture, scripting files and information on other key assets that I have used to develop this project as part of my portfolio and progressive development.


## **Project Overview** 

This project consists of AWS CodeBuild creation that automatically applies Terraform scripts whenever a commit change is made in the GitHub repository. The Terraform script uses an EC2 instance and creates an S3 bucket to as a means of CI/CD automation to also deploy a HTML website.


## **Tools used**

1. **IAM User:** CodeBuild will use User Credentials to authenticate with the AWS environemnt when the Build Project is being created
2. **Git:** Used to clone the provided files into the directory
3. **Terraform Script:**  The Terraform file provided will launch the EC2 instance and install the HTML website on it
4. **AWS CodeBuild:** To compile your source code and run CodeBuild job that will automatically apply a terraform script whenever I commit a change into a GitHub reposistory
5.  **AWS S3:** Enables environmental file storage.

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
1. Shell scripts will be created to install Terraform, configure a profile and run the Terraform command.
2. Open the project folder you have been working on as part of this project and create a new folder. All the CI/CD scripts will be contained within this folder 
3. Terraform will have to be installed in the container that CodeBuild will use as part of the project so the first Shell script that will be created is the Shell script which will be used to install Terraform on the container. This will require creating a new file within the new folder you would have create in step 11. For the purposes of this project the Shell script can be found in this repository and it is called 'install-terraform.sh'. Ensure to remain the file name with 'install-terraform.sh'. Copy the script contents within the file and paste it in the new file. Once you have pasted the content inside the file ensure to save it
4. the second Shell script this will be created is the Shell script that will be used to create a named profile in the container. Create another new file within the folder created in step 11. For the purposes of this project the Shell script can be found in this repository and it is called 'configure-named-profile.sh'. Ensure to remain the file name with 'configure-named-profile.sh'. Copy the script contents within the file and paste it in the new file. Once you have pasted the content inside the file ensure to save it
5. The third Shell script that will be created is the script used to create the Terraform command: Terraform init, Terraform apply and Terraform destroy. Create another new file in the folder created above. For the purpose of this project the Shell script can be found in this repository and it is called 'apply-terraform.sh'.  Ensure to remain the file name with 'apply-terraform.sh'. Copy the script contents within the file and paste it in the new file. Once you have pasted the content inside the file ensure to save it

### Personal Access Token Creation
1. Create a Personal Access Token in GitHub which will be used by the CodeBuild to access the files as part of the projecr job creation

### Creating the CodeBuild project
1. It’s highly recommended that if you haven't updated and pushed any updates to GitHub it’s wise to do so before completing this part
2. In the AWS Management console under services type CodeBuild and select click on Build Project. It’s wise to name the project the same as your GitHub Repo in the event you have multiple projects it’s easier to identify them for each project that you do. Also feel free to give a description
3. Under the Source Tab select GitHub and this is where the repo that was created earlier for the project is located. Select connect with a GitHub personal access token and enter in your personal access token that was created previously, then save token. It will now connect to your GitHub account
4. Select repository in my GitHub account and in the dropdown you will see all the repositories you’ve created. Choose the correct repo for your project
5. Under the Primary Source webhook events check rebuild every time a code change is pushed to this repo and leave it on single build. For the event type select push and pull request merge. This means anytime we push or pull a request to the repo it will rebuild the project
6. Under the Environment section choose manage image and for the Operating system select Amazon Linux. For the image select the latest image available
7. For the Environment variables in the configured-named-profile.sh file that was created previously is where you’ll find the information to implement into the CodeBuild environment variables section. This will include aws access key ID, secret access key, region and profile name. Enter in the values for each one. Enter in IAM user secret access key and ID information that was saved as well into the value section
8. The Buildspec section is where you’ll tell codebuild where the buildspec.yml folder is located. For my particular location it will be in my cicd folder so for the buildspec name give the correct location of your folder
9. Then click create build project. Now it will create the build project for you. Once the build has been created you can now see the name of it
10. Click Start Build and CodeBuild will clone the repo on the container and it will use the buildpec file to run the commands. This particular file will create an ec2 instance and run the website from the install-website.sh file onto the ec2 instance
11. If the build is a success and you now have the ability to view the outputs. CodeBuild has ran the commands and you can see the outputs through the build logs and phase details:
![Screenshot 2024-08-16 at 20 09 11](https://github.com/user-attachments/assets/18d302ff-b751-4870-b977-ca97ec67df45)

 ### Running Terraform destroy in the CodeBuild project
1. Now we can finally clean up the environment so the next step is to destroy the resources created in the build
2. Go back to VSCode and in the apply-terraform.sh file add a hashtag to the beginning of line 13 and for line 16 remove the hashtag at the beginning. This will automatically run the build job and instead of terraform apply it will run destroy
3. Save the file and update your file to GitHub. Type a commit message such as update file (click commit) and click sync this will initiate the build
4. Go Back to CodeBuild and in the latest build history you’ll see that it’s in progress and the status will let you know it was a success as well. You can see the build was successfully destroyed through the build logs and phase details once again:
![Screenshot 2024-08-16 at 20 35 22](https://github.com/user-attachments/assets/dd94bdf6-091a-4c51-821f-4f8d02fa89ad)
![Screenshot 2024-08-16 at 20 39 58](https://github.com/user-attachments/assets/bd7ba0a5-d1cc-4e9e-81d5-3ec2e1024f4d)

## **How to Use**

1. Clone this repository to your local machine.
2. Follow the AWS documentation to create the required resources (S3 Bucket IAM Management) as outlined in the architecture overview
3. Use the provided scripts to set up the reosurce and applications
4. Configure the reosurces assets as per the architecture
5. Access the Website website through the endpoint URL for your bucket

## **Additional Resources**

- **AWS Documentation:** Refer to the [AWS documentation](https://aws.amazon.com/documentation/) for detailed guides on setting up S3 Bucket, IAM roles and other services such as VPC, EC2, Auto Scaling, and Load Balancer
- **GitHub Repository Files:** Refer to [Otite-Git/-Host-a-Static-Website-on-AWS-S3-Bucket-With-Terraform](https://github.com/Otite-Git/CI-CD-Project-using-AWS-CodeBuild--and-S3-for-Terraform-Script-Automation.git) to access the repository files for scripts, architectural diagrams, and configuration files necessary for deploying the website.

## **Contributing**

Contributions to this project are welcome! Please fork the repository and submit a pull request with your enhancements

## **License**

This project is licensed under the MIT License - see the LICENSE file for details

## **What problems did I solve by completing this project?**

1. **Simplicity:** I was able to effectively to simplift the creation of the hosting of the website through automating the deployment process using Terraform by reducing manual effort and ensures consistency across environments as the deployment of infrastructure and website hosting can be error-prone and time-consuming
   

## **What issues did I face while working on the project and how did I resolve that issue?**
  
- **Terraform Configuration Errors:** I had faced the issue of Syntax errors and incorrect configuration in Terraform files. I was able to resolve both issues by using Terraform validate and terraform plan commands to check for errors and view changes before applying them

- **Terraform file setup Error:** Initially when starting the project, I had faced the challenge of my created main.tf file not being picked up or when entering the terraform apply command. I would get an error message stating the file could not be found in my directory despite it being there. I had resolved this issue by creating a new copy of the file and saving it in VS Code ensuring the Terraform logo appeared after it was correctly formatted. I then uploaded it into the directory folder and ran the Terrafrom apply command again. After doing this it had successfully worked
 

 ## **What overall lessons did I learn?**
 
- **AWS IAM (Identity and Access Management):** Understanding the role of IAM in securing and managing access to AWS resources. Creating IAM roles and policies to grant necessary permissions for Terraform to manage AWS resources

- **Terraform Basics:** Infrastructure as Code (IaC): Understanding how to define and manage infrastructure using code. Terraform Configuration: Learning the syntax and structure of Terraform configuration files (e.g., .tf files)





