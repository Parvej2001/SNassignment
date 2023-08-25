# CI/CD Pipeline Setup for a Node App

This repository contains the setup and documentation for the CI/CD pipeline of the Node App using Jenkins , Docker, Aws Ec2.

![image](https://github.com/Parvej2001/SNassignment/assets/86014533/78809f2b-6613-4847-8a68-1e1a64cc094b)

## Overview

The purpose of this pipeline is to automate the process of building, testing, and deploying the App using a CI/CD tool. The pipeline is triggered automatically whenever there are code commits to the main branch of the repository.
## Pipeline Steps

1. **Source Code Integration**: The pipeline is configured to monitor the main branch of the repository for any new code commits. Upon detecting a new commit, it automatically triggers the pipeline.

2. **Unit Tests**: The pipeline executes unit tests using the test suite provided within the project. Test results are reported using JUnit format.

3. **Docker Image Build**: Upon successful completion of unit tests, the pipeline builds a Docker image of the App. The Docker image includes the necessary dependencies and configurations to run the application.

4. **Deployment to Staging Environment**: After building the Docker image, the pipeline deploys the image to a cloud-based staging environment here we have AWS EC2 

## Setup Instructions

**Step 1--** Create an AWS EC2 T2 Micro Instance(Free Tier)with Ubuntu Image and SSH into it. You can create a new key-pair or use an existing one. Ensure to enable HTTP/HTTPS traffic.

**Step 2--** Install Jenkins in your AWS EC2 Instance.
        - [Jenkins Installation Guide](https://jenkins.io/doc/book/installing/)
        
**Step 3--** Allow Port 8080 in the Security Group on EC2 Instance as Jenkins works on Port 8080

**Step 4--** To unlock Jenkins, goto sudo cat /var/lib/jenkins/secrets/InitialAdminPassword

Copy the password and click on continue

i. Create a New Jenkins Job:
   - Name: SN-task1 (You can write any)
   - Type: Freestyle project
![image](https://github.com/Parvej2001/SNassignment/assets/86014533/7df77f62-d248-4ee0-ab9a-e51f69fedf5c)

ii. Configure Source Code Integration:
   - Choose Git as the version control system.
   - Provide the repository URL and select the main branch.
   - Add appropriate credentials if required.
![image](https://github.com/Parvej2001/SNassignment/assets/86014533/ae8c3b1b-958b-4c73-8afc-b6b737a0cea3)

**Step 5--** Integrate Github and Jenkins

This will ensure that our code has been integrated with Jenkins now.
We will need to generate SSH key. Goto your EC2 Instance and type #ssh-keygen

We will see a Private key and a Public key generated. We will need to give the Public key to Github.

Goto Github settings ->SSH and GPG Keys-> Generate new key and label it is Jenkins-Project. Add the public key here and add the keys.

And click on build now. You will see the pipeline getting built under console output like this

![image](https://github.com/Parvej2001/SNassignment/assets/86014533/5494aab5-a0fd-498d-b4a0-39a800c41349)

**Step 6--** With the help of Dockerfile, we can automate these steps.
--To install Docker , Run these commands:

`sudo apt-get install docker.io` And Create a Dockerfile as its there in the repo.

Now we need run the dockerfile using command ` docker build . -t any name `
      
Congratulations, continuous Integration is now done.

**Step 7 --** Automate the entire steps in Jenkins

Dashboard -> todo-node-app->Configuration -> Build Steps->Add Build step->Execute shell

The steps that we did manually have to be executed via Shell for automation

`docker build . -t task1-app`

`docker run -d --name node-task1-app -p 8000:8000 task1-app`

and finally save, and Run. Finally, we have automated the building of Dockerfile using Jenkins. We have now finished continuous integration and continuous delivery.

**Step 8--** Integrate GitHub and Webhook. We will need to install the plugin. Go to Manage Jenkins → Manage Plugins → Type in GitHub Integration. Install without restart

![image](https://github.com/Parvej2001/SNassignment/assets/86014533/2aa7d75f-8965-465f-97f3-8a6ecf33de7a)

Go to the Repository settings, and add webhook. In the Payload URL, give the Jenkins URL

…………………………../github-webhook/. In content type, make it application /json and add webhook.


Run these commands:


`sudo apt install nodejs`


`sudo apt install npm`


`sudo npm install`

`node app.js`

