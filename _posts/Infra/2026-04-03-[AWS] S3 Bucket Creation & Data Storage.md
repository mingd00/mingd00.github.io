---
title: "[AWS] S3 Bucket Creation & Data Storage"
last_modified_at: 2026-04-03
categories:
    - Infra
---

# AWS S3
> Amazon Simple Storage Service(Amazon S3) is an object storage service that offers industry-leading scalability, data availability, and performance. With virtually unlimited storage capacity, it allows you to securely store all types of data, including images, videos, and log files.
> 

<br>

### Bucket and Object
- Bucket: The top-level container where data is stored
    - General Purpose Buckets: The standard option used for general use cases. (images, videos, logs, backup data, etc.)
    - Directory Buckets: Delivering over 10 times higher performance than General Purpose Buckets, this type is optimized for high-performance computing and training machine learning models.
    - Table Buckets: A type designed specifically for large-scale data analytics.
    - Vector Buckets: Specialized for generative AI and LLM applications, this type is built to store and mange vector embedding values.
- Object: The fundamental storage unit consisting of data and metadata. Every object is contained within a bucket, and each object is idenitified by a unique key. 

<br>

### Accessing the S3 Console 

![image](/assets/images/5/1.png)

<br>

### Selecting a Region
- Once a bucket is created, its AWS Region cannot be changed. Therefore, it is highly recommended to select the Region closest to your infrastructure to maximize time and cost efficiency.

![image](/assets/images/5/2.png)

<br>

### Creating a Bucket
- General purpose buckets > Create bucket

![image](/assets/images/5/3.png)

<br>

- Configuring namespace and name  

![image](/assets/images/5/4.png)

First, set the namespace. The Global namespace checks uniqueness based on users worldwide, while the Account Regional namespace checks it based on your own account.

The Account Regional namespace option offers more flexibility in naming and is the method recommended by AWS.

<br>

- Object Ownership

Determines whether to enable ACLs. While Access Control Lists manage access permissions to buckets and objects, they complicate management. Therefore, it's recommended to keep them disabled unless there is a specific reason.

<br>

AWS strongly recommends using IAM policies or bucket policies instead of ACLs.

![image](/assets/images/5/5.png)

<br>

- Block Public Access settings

This is a powerful security layer that prevents S3 data from being exposed to the outside. it's recommended to always keep it turned on unless there is an exceptional case. 

<br>

However, this setting must be turned off if the purpose is website image hosting, static website hosting, or providing public data.

![image](/assets/images/5/6.png)

<br>

- Versioning

This is an option that determines whether to allow the same object within the same bucket. When enabled, even if the identical object is uploaded, it is managed by dividing it into different versions. 

![image](/assets/images/5/7.png)

<br>

- Tags 

Tags can also be configured for cost tracking.

![image](/assets/images/5/8.png)

<br>

- Encryption settings

For the Encryption type, I selected the SSE-S3 method, where AWS manages everything.

Enabling the Bucket Key works as a cache and drastically reduces costs, so it is best to keep it set to enable unless there is a specific reason not to. 

![image](/assets/images/5/9.png)

<br>

- Create Bucket

![image](/assets/images/5/10.png)

<br>

### Upload Object

- Bucket > General purpose bucket > Upload

![image](/assets/images/5/11.png)

<br>

- Upload file

![image](/assets/images/5/12.png)

<br>

- Success

![image](/assets/images/5/13.png)
