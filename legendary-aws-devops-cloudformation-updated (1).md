<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Infrastructure as Code with CloudFormation

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-devops-cloudformation-updated)

**Author:** Oluwaferanmi Ayanwale  
**Email:** oluwaferanmiayanwale@gmail.com

---

![Image](http://learn.nextwork.org/intense_lavender_witty_crocodile/uploads/aws-devops-cloudformation-updated_bd8b836b)

---

## Introducing Today's Project!

In this project, I will demonstrate how to set up a CloudFormation template. I'm doing this project to learn more about IaC and how to do this for CI/CD architecture. By the end of this project, resources like CodeArtifact, CodeBuild, CodeDeploy, CodeConnection, and more will be defined together in a single template.

### Key tools and concepts

Services I used were CloudFormation, CodeArtifact and the Code suites of services. Key concepts I learnt include Infrastructure as Code, how to use the IaC generator, resolving circular dependencies and resources that might depend on other resources to be created first. I also learnt how to write my own resource definitions in the secrets mission.

### Project reflection

This project took me approximately 2 hours to complete. The most challenging part was editing the resources I could not originally add to the template like the CodeDeploy group. This is because the resource is complex in nature and would need a lot of settings to configure. It was most rewarding to see my CloudFormation template deployed and live.

This project is part six of a series of DevOps projects where I'm building a CI/CD pipeline! I'll be working on the next project tomorrow.

---

## Generating a CloudFormation Template

The IaC Generator is a tool in the CloudFormation console that helps with writing CloudFormation templates faster. It works in a three-step process where the IaC generator first scans the resources, then lets us create a template based on the resources found, and finally lets us launch that template with the resources created in that template.

A CloudFormation template is a text file that defines resources I want to deploy inside. The resources that I did add to my template include CodeArtifact (domains and repos), CodeDeploy Application, IAM roles and policies, S3 bucket. 

The resources I could not add to the template were CodeBuild projects and CodeDeploy deployment groups. This is because both resources are complicated. I would have to write them manually.

![Image](http://learn.nextwork.org/intense_lavender_witty_crocodile/uploads/aws-devops-cloudformation-updated_0495b046)

---

## Template Testing

Before testing my template, I deleted the existing resources from my account because they share the same name as the resources in the generated template, this clash would cause an error. So, I am deleting the resources to avoid the overlap.

I tested my template by launching a stack using the template I generated. The result of my first test was 'create failed'. because my codeconnections was set to a different region.

![Image](http://learn.nextwork.org/intense_lavender_witty_crocodile/uploads/aws-devops-cloudformation-updated_f56730fd)

---

## DependsOn

To resolve the error, I opened up the template in a code editor to try to update the template manually. The DependsOn attribute means a resource needs to wait for another resource in the same template to be created first.

The DependsOn line was added to four different parts of my template. It was all four policies for CodeBuild which are policies that allow access to CodeArtifact, CodeConnection, CloudWatch and EC2 instances. For CodeArtifact policy, I had to define 2 'depends on' line, that is: depends on the CodeBuild and EC2 instance service role.

![Image](http://learn.nextwork.org/intense_lavender_witty_crocodile/uploads/aws-devops-cloudformation-updated_f0df8018)

---

## Circular Dependencies

I gave my CloudFormation template another test! But this time, there was a new error concerning circular dependencies. This error states that CloudFormation does not know what resource to deploy first, as the policies depend on the roles, but the roles depend on the policies to be created first. So CloudFormation is complete.

To fix this error, I revisited the template and tried to understand why both roles and policies are referenceing each other in the template. As it turns out, the roles have a section called 'managepolicyarn' that references the policy they use, then the policy definitions have the depends on line that asks to wait for the roles to be created first. To resolve this loop, I simply deleted all of the 'managepolicyarn' sections from the roles.

![Image](http://learn.nextwork.org/intense_lavender_witty_crocodile/uploads/aws-devops-cloudformation-updated_e6fd85ed)

---

## Manual Additions

In a project extension, I manually defined two more resources (a CodeBuild project and a CodeDeployment group).

I also had to make sure the references were consistent in this template, so I edited the values for the S3 bucket ID, CodeDeploy application ID, and service role IDs to match the ID of those resources in the template.

I also introduced Parameters, which are form fields in a CloudFormation template. Instead of hardcoding the values, we can get the CloudFormation stack to ask the user for the value of 'xyz' when I launch the resources.

![Image](http://learn.nextwork.org/intense_lavender_witty_crocodile/uploads/aws-devops-cloudformation-updated_1cee0428)

---

## Success!

I could verify all the deployed resources by visiting the resources section in the CloudFormation console and clicking on the hyperlinks created for each resource. I can see all resources created, beginning from the IAM resources to the CodeDeploy application.

![Image](http://learn.nextwork.org/intense_lavender_witty_crocodile/uploads/aws-devops-cloudformation-updated_bd8b836b)

---

---
