## Amazon S3 Service
![My project copy_latif](https://user-images.githubusercontent.com/98215575/152984978-5e0d386a-9c11-43b6-bb07-70a1733cf6c9.jpg)



- A database avaliable on AWS
- Can store any data type
- Can be used for DR(disaster recovery)
- Highly Avaliable and scalable 
- Can apply the crud actions.
How to connect:

- ssh into instance
- Enter VM
- Check python version with `python --version`
- Install `python3-pip` (Python version needs to be 3 or higher for aws cli to work)
- Create `alias python=python3`
- `sudo pip3 install awscli`
- Next `aws configure`
- Input access id and key
- Region: eu-west-1
- Language: `json`
- If details have been entered correctly all files will be listed in our specific s3 bucket.
