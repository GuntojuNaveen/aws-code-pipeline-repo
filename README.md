# aws-code-pipeline-demo
A sample Python Flask application with a complete CI/CD pipeline using AWS CodePipeline, CodeBuild, and CodeDeploy. This project demonstrates how to automate builds, manage secrets with Parameter Store, push Docker images to Docker Hub, and deploy seamlessly to AWS infrastructure.
****
## Set Up GitHub Repository
The first step in our CI journey is to set up a GitHub repository to store our Python application's source code. If you already have a repository, feel free to skip this step. Otherwise, let's create a new repository on GitHub by following these steps:

- Go to github.com and sign in to your account.
- Click on the "+" button in the top-right corner and select "New repository."
- Give your repository a name and an optional description.
- Choose the appropriate visibility option based on your needs.
- Initialize the repository with a README file.
- Click on the "Create repository" button to create your new GitHub repository.
- Great! Now that we have our repository set up, we can move on to the next step.
*****
# Code build setup
- Create CodeBuild project → Give a name,select default project and add description.
  
  ![Pipeline Screenshot](images/build1.jpeg)

- Choose source as github and select **Repository in my github account**  and after giving details it will ask for oauth permission, confirm that.
- 
  ![Pipeline Screenshot](images/build3.jpeg)
  
  ![Pipeline Screenshot](images/build2.jpeg)

- select single build here make sure **rebuild every time when a code change is pushed to the repository** is selected.

  ![Pipeline Screenshot](images/build4.jpeg)

- In this environment section  select ondemand,managed image and compute as EC2 , running mode as ec2 instance ,  Os as linux. and select new service role.
  Aws will create service role automatically if you already have service role then select existing service role.

  ![Pipeline Screenshot](images/build5.jpeg)

  ![Pipeline Screenshot](images/build6.jpeg)

- here write the buildspec file , if you already have builspec file present on github then select use buildspec file.

  ![Pipeline Screenshot](images/build7.jpeg)

- After creating codebuild project you will get the following details.

  ![Pipeline Screenshot](images/build9.jpeg)

- Now Go to Aws system manager, create parameter store and Save Docker username, password, and registry URL as SecureString.

  ![Pipeline Screenshot](images/build10.jpeg)

  ![Pipeline Screenshot](images/build11.jpeg)

- After creating parameters

  ![Pipeline Screenshot](images/build12.jpeg)

- Now to test the code build click on start build and check whether build is hapenning or not properly. here you will get error becuase we haven't given ssm permission to service role which was created in build step.

  ![Pipeline Screenshot](images/build13.jpeg)

- Now go to IAM -> Roles -> select service role -> attach Amazon SSM full access to service role

  ![Pipeline Screenshot](images/build14.jpeg)

  ![Pipeline Screenshot](images/build15.jpeg)

- after attaching permssions to service role codebuild will be successful.

  ![Pipeline Screenshot](images/build16.jpeg)


  

  
  
  
  

  
