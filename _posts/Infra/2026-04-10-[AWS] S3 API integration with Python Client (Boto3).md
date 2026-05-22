---
title: "[AWS] S3 API integration with Python Client (Boto3)"
last_modified_at: 2026-04-10
categories:
    - Infra
---

# AWS Authentication
> To integrate S3 API, you must authenticate using either the IAM Console or AWS CLI. I established the connection using the AWS CLI.
> 

<br>

- Installing the AWS CLI (Linux)

[Go to Installation](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)

```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```
<br>

- Verify Installation

![image](/assets/images/6/1.png)

<br>

- Authentication via AWS CLI

Since permissions are configured in IAN Identity Center, access is granted by appending sso.

```bash
aws configure sso
```

<br>

By Entering the information below, you can access the login page and complete authentication. This information can be found under IAM Identity Center > Dashboard.

![image](/assets/images/6/2.png)

<br>

If pop-up appears asking to connect to an external page, click "Open" and allow access.

![image](/assets/images/6/3.png)

![image](/assets/images/6/4.png)

<br>

Once account ID appears in the terminal, enter the additional information to establish a successful connection. 

![image](/assets/images/6/5.png)

<br>

- Check connection

```bash
aws sts get-caller-identity --profile [profile name]
```

![image](/assets/images/6/6.png)

=> If the user information is displayed in JSON, the configuration is successful.

<br>

### Install boto3

##### Install boto3 to integrate Python with the S3 API 

<br>

- Create and activate a virtual environment

```bash
python3 -m venv .venv
source .venv/bin/activate
```

<br>

- Install boto3

```bash
pip install boto3
```

<br>

### Establish a Session 

[Credentials - Boto3 1.42.76 documentation](https://docs.aws.amazon.com/boto3/latest/guide/credentials.html)

```bash
import boto3

session = boto3.Session(profile_name='AdministratorAccess-578673727079')
s3_client = session.client('s3')
```

=> If you run this file and no errors occur the connection is successful.

<br>

### Actions

- The S3 API is now ready for use. Refer to the official documentation below to call the functions required for your needs.
- The following examples demonstrate only a few of the available features, using only the required parameters. For additional options or detailed configurations, please consult the official documentation. 

[S3 - Boto3 1.42.77 documentation](https://docs.aws.amazon.com/boto3/latest/reference/services/s3.html)

<br>

##### List Buckets

```python
bucket_name = 'my-bucket-578673727079-ap-northeast-2-an'
bucket = s3_client.list_buckets()
```

<br>

##### Get bucket location

```python
location = s3_client.get_bucket_location(Bucket=bucket_name )
location['LocationConstraint']
```

<br>

##### Create bucket

```python
s3_client.create_bucket(
    Bucket='new-bucket',
    CreateBucketConfiguration={
        'LocationConstraint': 'ap-northeast-2'
    }
)
```

=> At this time, the bucket name must be globally unique. If the location is not specified, it defaults to us-east-1, so you must explicitly set your current location.

<br>

##### Delete bucket

```python
s3_client.delete_bucket(Bucket=bucket_name)
```

=> However, the bucket must be completely empty before it can be deleted. 

<br>

##### Get all objects

```python
response = client.list_objects(
    Bucket=bucket_name
)
```

<br>

##### Get a single objects

```python
response = s3_client.get_object(
    Bucket=bucket_name,
    Key='favicon.ico'
)
```

<br>

##### Create object (memory data -> file)

- Create an object directly from a string variable

```python
s3_client.put_object(
    Bucket=bucket_name, Key='note.txt', Body='Hello Office!'
)
```

![image](/assets/images/6/7.png)

<br>

##### Create object (upload file)

```python
s3_client.upload_file(
    Bucket=bucket_name, Filename='img/desktop.png', Key='desktop.png'
)
```