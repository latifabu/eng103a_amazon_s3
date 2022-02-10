## Amazon S3 Service
![My project s3](https://user-images.githubusercontent.com/98215575/153356300-c716d9b8-ddac-4422-982d-9e0f4537c4f0.png)



- A database avaliable on AWS
- Can store any data type
- Can be used for DR(disaster recovery)
- Highly Avaliable and scalable 
- Can apply the crud actions.

How to connect:

- ssh into EC 2instance
- Enter VM
- Check python version with `python --version`
- Install `python3-pip` (Python version needs to be 3 or higher for aws cli to work)
- Create `alias python=python3`
- `sudo pip3 install awscli` 
- Next `aws configure`
- Input access id and key
- Region: `eu-west-1`
- Language: `json`
- If details have been entered correctly all files will be listed in our specific s3 bucket.

### CRUD and buckets 
Commands used:
    
-  Create a bucket `aws s3 mb s3://<bucket-name>`(Naming convention in awscli uses "-" rather than "_" for spaces  )
    
-  Remove bucket with `aws s3 mb s3://eng103a-latif-devops` (buckets need to be empty to be removed)

- Use to remove files from a bucket - `aws s3 rm s3://<bucket-name>/[file-name]`

- Another command NOT RECOMMENDED if bucket content has multiple files aws s3 `rm s3://<bucket-name> --recursive` removes all files from bucket.


### CRUD using python script

- 1) In the terminal `pip3 install boto3`
- 2) Create a python file  `nano <file_name>.py`

`https://boto3.amazonaws.com/v1/documentation/api/latest/guide/s3-example-creating-buckets.html`

```
#!/usr/bin/env python3

import boto3
bucket_name = "eng103a-latif-boto3"
location = {'LocationConstraint': "eu-west-1"}

# creates bucket
s3 = boto3.resource('s3')
s3.create_bucket(Bucket=bucket_name, CreateBucketConfiguration=location)

# downloads file
s3 = boto3.client('s3')
s3.download_file('eng103a-name-devops', 'file.txt')

# delete object in bucket

s3 = boto3.resource('s3')
s3.Object('eng103a-name-devops', 'test.txt').delete()

# delete object

client = boto3.client('s3', region_name='eu-west-1')
bucket_name = 'eng103a-name-devops'
client.delete_bucket(Bucket=bucket_name)


```

To automate the process above:

```
#!/usr/bin/env python
import boto3
bucket_name = "eng103a-latif-devops"
location = {'LocationConstraint': "eu-west-1"}
s3 = boto3.resource('s3')
bucket_name = input("S3 Bucket Name\n")

while True:
    action = input("Type:[mb] Make a bucket, [rb] Remove a bucket, [d] Delete a file, [u] Upload a file, [dl] Download a file, [e] Exit Script\n")

    if action == "rb":
        s3.Bucket(bucket_name).delete()
    elif action == "mb":
        s3.create_bucket(Bucket=bucket_name, CreateBucketConfiguration=location)
    elif action == "d":
        filename = input("what is the filename?\n")
        s3.Object(bucket_name, filename).delete()
    elif action == "u":
        filename = input("what is the name of the file you're uploading?\n")
        targetfilename = input("what is the destination file name?\n")
        s3.Bucket(bucket_name).upload_file(filename, targetfilename)
    elif action == "dl":
        filename = input("what is the name of the file you're downloading?\n")
        targetfilename = input("what is the destination file name?\n")
        s3.Bucket(bucket_name).download_file(filename, targetfilename)
    elif action == "e":
        break
    else:
        print(\n"Please enter from the following options please")

```
## Auto Scaling Group (ASG) and load balancing
![My project s3](https://user-images.githubusercontent.com/98215575/153360096-6e5e1ed1-7cae-4654-bb06-be1be2a6735e.png)

