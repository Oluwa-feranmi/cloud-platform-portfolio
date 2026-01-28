<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Launch a Kubernetes Cluster

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-compute-eks1)

**Author:** Oluwaferanmi Ayanwale  
**Email:** oluwaferanmiayanwale@gmail.com

---

## Launch a Kubernetes Cluster

![Image](http://learn.nextwork.org/intense_lavender_witty_crocodile/uploads/aws-compute-eks1_e5f6g7h8)

---

## Introducing Today's Project!

In this project, I will deploy a Kubernetes cluster using AWS EKS because EKS is a service for deploying Kubernetes cluster in the cloud. I also get to use other tools like eksctl and CloudFormation.

### What is Amazon EKS?

### One thing I didn't expect

### This project took me...

---

## What is Kubernetes?

Kubernetes is a container orchestration tool that automates the management of containers. Companies and developers use Kubernetes to deploy and manage large-scale containerized applications.

I used eksctl to create a Kubernetes cluster using the CLI. The create cluster command I ran defined the name, node groups, node size settings, and region where my cluster will be created.

I initially ran into two errors while using eksctl. The first one was because I hadn't installed eksctl into my CLI. The second one was because I hadn't given my EC2 instance permission to create a Kubernetes cluster.

![Image](http://learn.nextwork.org/intense_lavender_witty_crocodile/uploads/aws-compute-eks1_ff9bfc221)

---

## eksctl and CloudFormation

CloudFormation helped create my EKS cluster because 'eksctl' uses CloudFormation to create the cluster when I run an 'eksctl' command. It created VPC resources because creating the EKS cluster in my default VPC will require a lot of networking configuration that can lead to human errors, compactibility and permissions issues.

Initially, there was no node group CloudFormation stack; I had to enable an Amazon VPC CNI plug-in from the EKS page for the node group to have the networking capabilities to link up well with my cluster. As a result, I have two CloudFormation stacks, one for the cluster and the other for the node group. The difference between a cluster and a node group is that the cluster is the entire Kubernetes setup, including the control panel and plane, while the node group is a group of EC2 instances inside.

![Image](http://learn.nextwork.org/intense_lavender_witty_crocodile/uploads/aws-compute-eks1_w3e4r5t6)

---

## The EKS console

I had to create an IAM access entry to see the nodes in the new node group. An access entry is a mapping of AWS IAM policies to the Kubernetes access control system. I set it up by using the access entry page in the EKS console.

It took at least 30 minutes to create my cluster, including some troubleshooting. Since I'll create this cluster again in the next project of this series, maybe this process could be sped up if I use templates (CloudFormation or Terraform), add the necessary plug-ins, and install 'eksctl.'

![Image](http://learn.nextwork.org/intense_lavender_witty_crocodile/uploads/aws-compute-eks1_e5f6g7h8)

---

## EXTRA: Deleting nodes

---

---
