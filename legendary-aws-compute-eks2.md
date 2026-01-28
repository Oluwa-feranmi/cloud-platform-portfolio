<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Set Up Kubernetes Deployment

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-compute-eks2)

**Author:** Oluwaferanmi Ayanwale  
**Email:** oluwaferanmiayanwale@gmail.com

---

## Set Up Kubernetes Deployment

![Image](http://learn.nextwork.org/intense_lavender_witty_crocodile/uploads/aws-compute-eks2_45e6c3de5)

---

## Introducing Today's Project!

In this project, I will prepare a backend app for Kubernetes deployment because Kubernetes deployment requires apps to be containerised and there to be a container image. I will create the container image in this project.

### Tools and concepts

I used Amazon EKS, Git, Docker, ECR, and EC2 to prepare a backend app for deployment with Kubernetes. This includes, setting up an EKS cluster, cloning code from GitHub, building and pushing a Docker image to ECR.

### Project reflection

This project took me approximately 1 hour, including demo time and troubleshooting. My favourite part was seeing an image in my ECR repository.

Something new that I learnt from this experience was the way AWS services seamlessly integrate, and how it is easy to work with them all.

---

## What I'm deploying

To set up today's project, I launched a Kubernetes cluster. Steps I took to do this included launching an EC2 instance, installing eksctl, and modifying the IAM role on my instance to grant it admin access.

### I'm deploying an app's backend

Next, I retrieved the backend that I plan to deploy. An app's backend means the logic behind the app's frontend. I retrieved backend code by cloning the git repository it lies in.

![Image](http://learn.nextwork.org/intense_lavender_witty_crocodile/uploads/aws-compute-eks2_1ebb86c71)

---

## Building a container image

Once I cloned the backend code, my next step is to build a container image of the backend. This is because Kubernetes needs a container image for a successful app deployment. At the moment, I just have the raw code and not the image.

When I tried to build a Docker image of the backend, I ran into a permissions error because I am logged into the instance as the ec2-user, which was created automatically. The ec2-user can't run root user-level commands without sudo.

To solve the permissions error, I added the ec2-user to the Docker group. The Docker group is a group in Linux systems that grants a user permission to run Docker commands like 'docker build'.

![Image](http://learn.nextwork.org/intense_lavender_witty_crocodile/uploads/aws-compute-eks2_45e6c3de5)

---

## Container Registry

I'm using Amazon ECR in this project to store the container image. ECR is a good choice for the job because it is an AWS service that integrates well with other AWS services. This makes deployment easier.

Container registries like Amazon ECR are great for Kubernetes deployment because I get to store tagged images from a single source. This means that, whenever users or other services pull the container image, they can do it without a manual install.

![Image](http://learn.nextwork.org/intense_lavender_witty_crocodile/uploads/aws-compute-eks2_l2m3n4o5)

---

## EXTRA: Backend Explained

After reviewing the app's backend code, I've learnt that the app functions by extrating data from another API, but I also have an API in app.py that's responsible for others wanting access to the service.

### Unpacking three key backend files

The requirements.txt file lists all the dependencies and libraries that every container needs to install when it gets created.

The Dockerfile gives Docker instructions on how Docker should build the container image of the app. Key commands in this Dockerfile includes, commands on where to find dependencies to install requuirements.txt, and commands that will automatically run.

The app.py file contains three main parts: installing dependencies, formatting the data into JSON, and passing the formatted data back to the user.

---

---
