<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Deploy a Web App with CodeDeploy

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-devops-codedeploy-updated)

**Author:** Oluwaferanmi Ayanwale  
**Email:** oluwaferanmiayanwale@gmail.com

---

![Image](http://learn.nextwork.org/intense_lavender_witty_crocodile/uploads/aws-devops-codedeploy-updated_val-27)

---

## Introducing Today's Project!

In this project, I will demonstrate how to use CodeDeploy to deploy a web app. I'm doing this project to learn about how deployment works and how it can be automated using a combination of CodeDeploy and Deployment scripts. By the end of this project, we will see a live website.

### Key tools and concepts

Services I used were CodeDeploy, CodeBuild, CodeArtifact, IAM, EC2, CloudFormation, S3, CodeConnection, VS Code and GitHub. Key concepts I learnt include deployment, deployment groups, deployments scripts, appspec, and the importance of rebuilding your project before you deploy.

### Project reflection

This project took me approximately 3 including demo time and troubleshooting. The most challenging part was understanding the separation of the deployment instance from the development instance. It was most rewarding to actually view my live web app and see how all the services used worked hand-in-hand to display the web app.

This project is part five of a series of DevOps projects where I'm building a CI/CD pipeline! I'll be working on the next project in a couple of hours.

---

## Deployment Environment

To set up for CodeDeploy, I launched an EC2 instance and VPC because they will make up our peoduction environment. We need to separate our development environment where we are testing the code from our deployment environment where we are deploying the web app so that the code does not get shown to  users until it is ready to be pushed to production.

Instead of launching these resources manually, I used CloudFormation. When I need to delete these resources, I can delete the entire stack. This will automatically delete the resources inside that stack.

Other resources created in this template include Networking resources like VPC, Internet Gateways, Route Tables, and Subnets. They're also in the template because production environments have specific requirements about traffic that should be enabled and blocked out. Setting up all of the networking resources that will help the deployment work is common practice.

![Image](http://learn.nextwork.org/intense_lavender_witty_crocodile/uploads/aws-devops-codedeploy-updated_val-5)

---

## Deployment Scripts

Scripts are mini programs that help automate the running of commands. To set up CodeDeploy, I also wrote scripts to automate deployment commands. That is, the commands the deployment EC2 Instance needs to run in order to host the web app.

The 'install_dependencies' will help the EC2 instance install all the dependencies it needs to host the web app, like Tomcat (the web server).

The start_server.sh will start up the 2 servers that are installed in the EC2 Instance. It starts up Tomcat for the Java app, then Apache (the webserver responsible for web traffic and passing requests to Tomcat).

The stop_server.sh will stop the Apache and Tomcat services when they are no longer needed to serve the web app to a user.

---

## appspec.yml

Then, I wrote an appspec.yml file to give CodeDepploy the instaurctions for deploying the web app. The key sections in appspec.yml are 'before install' (use the install dependecies scripts to install dependecies), 'application start' (use the start server script), and 'application stop' (use the stop server script).

I also updated buildspec.yml to tell CodeBuild that it should package up the new appspec.yml and set up scripts that were generated inside the buildartifacts.

![Image](http://learn.nextwork.org/intense_lavender_witty_crocodile/uploads/aws-devops-codedeploy-updated_val-12)

---

## Setting Up CodeDeploy

A deployment group is a group of EC2 instances that you can deploy to and also the collectin of settings that determine how you want to deploy your web app. A CodeDeploy application is simply a folder that holds together all the deployment groups for the same app.

To set up a deployment group, you also need to create an IAM role to permit CodeDeploy to access the EC2 instances it needs to coordinate. Otherwise, CodeDeploy will not have access to EC2 which also means not being able to give instances instructions to deploy the web app.

Tags are helpful for identifying the instances that will deploy the web app. I used the tag: Role = webserver to automatically match the EC2 instance deployed with the CloudFormation template.

![Image](http://learn.nextwork.org/intense_lavender_witty_crocodile/uploads/aws-devops-codedeploy-updated_val-18)

---

## Deployment configurations

Another key settings is the deployment configuration, which affects how quickly and risky the web app is deployed. I used CodeDeployDefault.AllAtOnce, so any changes that CodeDeploy deploys affects all of the instances in the deployment group at once.

In order to connect the deployment instance with CodeDeploy, a CodeDeploy Agent is also set up to receive instructrions from CodeDeploy and makes sure that the commands in appspec.yml are deployed.

![Image](http://learn.nextwork.org/intense_lavender_witty_crocodile/uploads/aws-devops-codedeploy-updated_val-20)

---

## Success!

A CodeDeploy deployment is a specific update to the application that is being deployed to users. The difference between a deployment and deployment group is that the group is like a settings file and the deployment is like a specific update made that is rolled out using the settings file.

I had to configure a revision location, which means where the web app's compressed file lives. My revision location was in the S3 bucket I created and linked with CodeBuild.

To check that the deployment was a success, I visited the IPv4 DNS address of the EC2 instance. I saw a live web app that is working and serving the web app code to end users.

![Image](http://learn.nextwork.org/intense_lavender_witty_crocodile/uploads/aws-devops-codedeploy-updated_val-27)

---

## Disaster Recovery

---

---
