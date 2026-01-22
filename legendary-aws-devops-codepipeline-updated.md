<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Build a CI/CD Pipeline with AWS

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-devops-codepipeline-updated)

**Author:** Oluwaferanmi Ayanwale  
**Email:** oluwaferanmiayanwale@gmail.com

---

![Image](http://learn.nextwork.org/intense_lavender_witty_crocodile/uploads/aws-devops-codepipeline-updated_fbdetger)

---

## Introducing Today's Project!

In this project, I will demonstrate how to use CodePipeline to set up a CI/CD pipeline. CodePipeline will AUTOMATE the flow from GitHub all the way to CodeDeploy. By the end of this project, I would be able to push code and see the updated web app's live changes without having to go to CodeBuild or CodeDeploy.

### Key tools and concepts

Services I used were CodePipeline, CodeDeploy, CodeDeploy, CodeArtifact, GitHub, VS Code, EC2, S3, CloudFormation, and IAM. Key concepts I learnt include the differenct stages in the CI/CD pipeline, handling rollbacks, and webhooks.

### Project reflection

This project took me approximately 3 hours, including troubleshooting and demo time. The most challenging part was probably the rollback on the CodePipeline, which was due to insufficient permissions, I had to update the permissions. It was most rewarding to see the live web app and confirm the update without having to build and deploy the project ourselves.

---

## Starting a CI/CD Pipeline

AWS CodePipeline is a tool that creates a workflow that automatically moves code from our source code repo (GitHub) all the way to CodeDeploy (our deployment tool). This makes sure deployments are consistent and reliable with less human errors.

CodePipeline offers different execution modes based on how multiple runs of the same pipeline are treated. I chose superseded, which means, I will focus on running the latest pipeline run that we start and cancel the older ones. Other options include 'queued' and 'parallel'.

A service role gets created automatically during setup so that CodePipeline has sufficient permissions to carry out its tasks without any setbacks.

![Image](http://learn.nextwork.org/intense_lavender_witty_crocodile/uploads/aws-devops-codepipeline-updated_gdnhtm)

---

## CI/CD Stages

The three stages I've set up in my CI/CD pipeline are 'source (the source code for the web project)', 'build', and 'deploy'.

CodePipeline organizes the three stages into a single diagram that showcases the flow of changes from source to deploy. In each stage, you can see more details on the pipeline execution that it belongs to, the service, and shortcuts to the connected service.

![Image](http://learn.nextwork.org/intense_lavender_witty_crocodile/uploads/aws-devops-codepipeline-updated_fbdetger)

---

## Source Stage

In the Source stage, the default branch tells CodePipeline exactly which version of the code I want to use in this workflow. In Production environments, we can have different branches to represent different versions of your code. By specifying a branch, we are making sure a specific version is getting deployed and not a random branch.

The source stage is also where you enable webhook events, which are like notifications whenever a change is made to the source code. The webhook events will detect the change and trigger CodePipeline to start a run.

![Image](http://learn.nextwork.org/intense_lavender_witty_crocodile/uploads/aws-devops-codepipeline-updated_sergt)

---

## Build Stage

The Build stage sets up how we build the web app and make it ready for deployment. I configured CodeBuild to be the build provider and to use the input artifact that was output by the source stage. The input artifact for the build stage is the compressed code that the source stage retrieved from GitHub and compressed to a .zip file.

![Image](http://learn.nextwork.org/intense_lavender_witty_crocodile/uploads/aws-devops-codepipeline-updated_j1k2l3m4)

---

## Deploy Stage

The Deploy stage is where I set up CodeDeploy to be the deployment provider. It takes the build artifact from CodeBuild and the application, plus deployment settings that were defined in the deployment group.

![Image](http://learn.nextwork.org/intense_lavender_witty_crocodile/uploads/aws-devops-codepipeline-updated_m4n5o6p7)

---

## Success!

Since my CI/CD pipeline gets triggered by code changes in the webhook events. I tested my pipeline by updating the code. I added a new line to the web app's index.jsp file and pushed the changes.

The moment I pushed the code change, CodePipeline responded immediately by triggering a new build and deploy stage. The commit message under each stage reflects the latest code change.

Once my pipeline executed successfully, I checked the live web app and confirmed that it updated without having to rebuild the project from CodeBuild and redeploy the project in CodeDeploy. The changes went live to production straight away.

![Image](http://learn.nextwork.org/intense_lavender_witty_crocodile/uploads/aws-devops-codepipeline-updated_e1f2g3h4)

---

## Testing the Pipeline

In a project extension, I initiated a rollback on the deploy stage. Automatic rollback is important for situations where you have deployed a change that passed tests but does not look the way it should.

During the rollback, the source and build stages are both stages that come before the deployment. I could verify this by comparing the commit messages related to each stage.

After the rollback, the live web app reverted to the previous version before I pushed the new changes.

![Image](http://learn.nextwork.org/intense_lavender_witty_crocodile/uploads/aws-devops-codepipeline-updated_sdfgsdfgdf)

---

---
