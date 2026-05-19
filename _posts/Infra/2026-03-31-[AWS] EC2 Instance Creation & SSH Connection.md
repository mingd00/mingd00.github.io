---
title: "[AWS] EC2 Instance Creation & SSH Connection"
last_modified_at: 2026-03-31
categories:
    - Infra
---

## Create Instance
### Console Access
- EC2 console > Dashboard > Launch instance

![image](/assets/images/4/1.png)
![image](/assets/images/4/2.png)

<br>

#### Name and tags
- Set instance name 

![image](/assets/images/4/3.png)

<br>

#### AMI(Amazon Machine Image)
An OS and software environment template for creating instances, similar to preparing materials for building a house.

I selected the default Amazon Linux 2023 AMI.

![image](/assets/images/4/4.png)

<br>

#### Instance type
Select hardware specifications like CPU, RAM, and network performance, similar to designing the number of rooms, room sizes, and electrical capacity when building a house.

I selected the default t3.micro, which is suitable for testing and falls within the Free Tier limits.

![image](/assets/images/4/5.png)

<br>

### Key pair
- Create key pair 

![image](/assets/images/4/6.png)

<br>

- Specify the key pair name, and then choose the key pair type and file format

![image](/assets/images/4/7.png)

<br>

- Once the key pair is created, the .pem file will be downloaded, and you should keep it in a secure location. (This file can only be downloaded once at the time of creation)

<br>

![image](/assets/images/4/8.png)

<br>

### Network
A vpc is the overall network, a subnet is a section divided by role within that network, and an instance is a virtual server running inside the vpc. 

Each instance is assigned an ip address, which can be used to configure access permissions.


![image](/assets/images/4/9.png)

<br>

- Review the summary, and click "Launch instance"

![image](/assets/images/4/10.png)

<br>

- Instance is successfully created when the success banner appears at the top

![image](/assets/images/4/11.png)

<br>

### SSH Connection
- Permission Configuration
```bash
chmod 400 test-instance-key-pair.pem
```

<br>

- Connection

![image](/assets/images/4/12.png)

<br>

### Connecting to SSH via MobaXterm
- Using MobaXterm allows you to connect without configuring permissions
- Go to Session > SSH, then set the Remote host, username, and private key path (The Remote host is the Public IP address)

![image](/assets/images/4/13.png)
![image](/assets/images/4/14.png)

<br>

### Terminate instance
- Instance > Instance state(top right corner) > Terminate instance

![image](/assets/images/4/15.png)

<br>

- Once the Instance state changes from "Shutting-down" to "Terminated", it has been successfully terminated

![image](/assets/images/4/16.png)
![image](/assets/images/4/17.png)