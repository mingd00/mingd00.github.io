---
title: "[AWS] AWS Core Services & IAM Identity Center Management"
last_modified_at: 2026-03-26
categories:
    - Infra
---

## What is AWS?

> Amazon Web Services is a cloud platform that allows you to rent IT infrastructure, such as servers, storage, databases, on-demand.
> 

<br>

## Core services

- **EC2 (Elastic Compute Cloud) → Server**
Virtual Linux servers where applications are executed.
- **S3 (Simple Storage Service) → File Storage**
Storage for images, videos, and data, managed independently of the server.
- **RDS (Relational Database Service) → Database**
Storing and managing data within a relational database.
- **IAM (Identity and Access Management) → Permission Management**
Configuring permissions for users and servers.
- **VPC (Virtual Private Cloud) → Network**
A private, virtual network environment created within AWS.

<br>

## IAM Identity Center

> From a security perspective, using a root account for everyday tasks is strongly discouraged.
with AWS IAM Identity Center, you can centrally manage permissions for multiple users across your organization.
You can manage access at the individual user level ot by organizing them into gruops, with the flexibility to define custom permission sets.
> 

<br>

#### Accessing IAM Identity Center

![image](/assets/images/3/3-1.png)

<br>

#### Activation

![image](/assets/images/3/3-2.png)

![image](/assets/images/3/3-3.png)

<br>

#### groups → create group

![image](/assets/images/3/3-4.png)

<br>

#### user → add user

![image](/assets/images/3/3-5.png)

![image](/assets/images/3/3-6.png)

<br>

#### Permission Management: Configuring permissions for created groups

Dashboard → Manage permissions

![image](/assets/images/3/3-7.png)

<br>

#### aws-accounts → select my account → Assign users or groups

![image](/assets/images/3/3-8.png)

<br>

#### Select the group for permission settings

![image](/assets/images/3/3-9.png)

<br>

#### Configure permission types.

I selected the AdministratorAccess option from the AWS managed policy templates. Custom permissions are also available if needed.

![image](/assets/images/3/3-10.png)

<br>

#### Select the group and permission set in order

![image](/assets/images/3/3-11.png)

![image](/assets/images/3/3-12.png)

<br>

#### Success

![image](/assets/images/3/3-13.png)

<br>

→ You can log in to the account with administrator privileges by accessing the link sent via email and registering your login information.

→ Accounts created in IAM Identity Center cannot be accessed through the standard AWS login page; they must be accessed via the Identity Center portal (AWS IAM Identity Center → AWS access portal URL).