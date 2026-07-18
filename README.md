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

- Now after successful Codebuild Go to your configured dockerhub and check whether image was updated in your repository.

  ![Pipeline Screenshot](images/build17.jpeg)

- Create code pipeline , select build custom pipeline

   ![Pipeline Screenshot](images/build18.jpeg)

- Enter pipeline name, execution mode as queued and select service role which will create automatically by AWS.

   ![Pipeline Screenshot](images/build19.jpeg)

- Now select Github via oauth app as Source provider and give repository name and branch.

   ![Pipeline Screenshot](images/build20.jpeg)

   ![Pipeline Screenshot](images/build21.jpeg)

- Select other build providers as codebuild , select project name which you already created in codebuild project , select build type as single build , region as mumbai , select input artifact as source artifact.

   ![Pipeline Screenshot](images/build22.jpeg)

- Verify all the details before click on create a pipeline.

   ![Pipeline Screenshot](images/build23.jpeg)

   ![Pipeline Screenshot](images/build24.jpeg)

- Now test the pipeline by changing something on the source github and create a commmit , then our pipeline will invoke the codebuild automatically.

   ![Pipeline Screenshot](images/build26.jpeg)

- Now the last step is to create codedeploy to deploy our application for that first create application on codedeploy by giving name of the application and choose compute platform as EC2/on-premises

  ![Pipeline Screenshot](images/build27.jpeg)

- create EC2 instance and don't forget to add tagname to the instance and enable public IP also.

  ![Pipeline Screenshot](images/build28.jpeg)

- After creating EC2 instance try to login to EC2 instance using its pem file and public ip on local terminal.

  ![Pipeline Screenshot](images/build29.jpeg)

- Now on EC2 instance, install necessary packages and install codedeploy agent and check the status of codedeploy agent
  ```
  sudo apt update
  sudo apt install ruby-full
  sudo apt install wget
  cd /home/ubuntu
  wget https://aws-codedeploy-ap-south-1.s3.ap-south-1.amazonaws.com/releases/codedeploy-agent_1.8.1-26_all.deb
  sudo dpkg -i --force-depends codedeploy-agent_1.8.1-26_all.deb
  chmod +x ./install
  sudo ./install auto
  sudo systemctl enable codedeploy-agent
  sudo systemctl start codedeploy-agent
  sudo systemctl status codedeploy-agent
  ```

  ![Pipeline Screenshot](images/build30.jpeg)

  


  


 

  






  





  

  
  
  
  

  
