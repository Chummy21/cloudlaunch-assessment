### NAME: Sylvia Chioma Okafor

### ALTSCHOOL ID: ALT/SOE/024/4939

## Cloudlaunch-Assessment
This repository contains my implementation of CloudLaunch, a project demonstrating core AWS skills. The project covers:

Static Website Hosting on S3 – Hosting a public website securely with read-only access for anonymous users, private storage for sensitive documents, and a visible-but-restricted bucket.

📌 IAM User Management – A custom IAM user with limited, precise permissions for secure access control across the three S3 buckets.

📌 VPC Design – A logically separated VPC with public, app, and database subnets, internet gateway, route tables, and security groups to demonstrate secure network architecture.

📌 All resources are created within the AWS Free Tier and follow best practices for access control and network segmentation.

## Task 1: Static Website on S3 + IAM

- **Buckets I created**:
  - `cloudlaunch-site-bucketchioma` (public read for website)
  - `cloudlaunch-private-bucketchioma` (private; IAM user Get/Put only; no Delete)
  - `cloudlaunch-visible-only-bucketchioma` (listable by IAM user; contents not accessible)
  - ![Buckets Created](./images/s3%20buckets.png)

- **Website link**:
  - Created an HTML Document which I used to host my static website. The wesite is publicly accessible and for read-only anonymous users.
  - S3 website endpoint: [s3-website-endpoint](http://cloudlaunch-site-bucketchioma.s3-website-eu-west-1.amazonaws.com)

  - **Bonus (if used)**
  - I also set up a CloudFront distribution in front of this bucket for HTTPS and global caching
  - CloudFront URL: [CloudFront URL](https://d2iqpmag3z7xtd.cloudfront.net/)`
  - CloudFront Creation
  - ![CloudFront](./images/cloud%20front%20distribution.png)

  - Here, I created an IAM User
  - **IAM user**: `cloudlaunch-user`
  - Console sign-in URL: `https://<chiomagerald+aws@gmail.com>.signin.aws.amazon.com/console`
  - Username: `cloudlaunch-user`
  - Temporary password: 

> ⚠️ Security note: The user I created is highly restricted and created only for grading. After grading, the user will be **deleted**.



- **IAM policy JSON** (attached to `cloudlaunch-user`):
- This policy was attached to the three buckets( Cloudlaunch-publicly-accessible-bucket, Cloudlaunch-visible-only-bucket and Cloudlaunch-private-bucket)
```json File used is shown below

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "S3ListBucketsInConsole",
      "Effect": "Allow",
      "Action": "s3:ListAllMyBuckets",
      "Resource": "*"
    },
    {
      "Sid": "S3ListSpecificBuckets",
      "Effect": "Allow",
      "Action": "s3:ListBucket",
      "Resource": [
        "arn:aws:s3:::cloudlaunch-site-bucket",
        "arn:aws:s3:::cloudlaunch-private-bucket",
        "arn:aws:s3:::cloudlaunch-visible-only-bucket"
      ]
    },
    {
      "Sid": "S3ReadSiteContent",
      "Effect": "Allow",
      "Action": ["s3:GetObject"],
      "Resource": "arn:aws:s3:::cloudlaunch-site-bucket/*"
    },
    {
      "Sid": "S3ReadWritePrivateNoDelete",
      "Effect": "Allow",
      "Action": [
        "s3:GetObject",
        "s3:PutObject"
      ],
      "Resource": "arn:aws:s3:::cloudlaunch-private-bucket/*"
    },
    {
      "Sid": "S3ExplicitDenyDeleteEverywhere",
      "Effect": "Deny",
      "Action": "s3:DeleteObject",
      "Resource": [
        "arn:aws:s3:::cloudlaunch-site-bucket/*",
        "arn:aws:s3:::cloudlaunch-private-bucket/*",
        "arn:aws:s3:::cloudlaunch-visible-only-bucket/*"
      ]
    },
    {
      "Sid": "VPCReadOnly",
      "Effect": "Allow",
      "Action": [
        "ec2:DescribeVpcs",
        "ec2:DescribeSubnets",
        "ec2:DescribeRouteTables",
        "ec2:DescribeInternetGateways",
        "ec2:DescribeSecurityGroups",
        "ec2:DescribeVpcAttribute"
      ],
      "Resource": "*"
    }
  ]
}

---

- I Created a restricted IAM user cloudlaunch-user with read/write access to cloudlaunch-private-bucket, read-only access to cloudlaunch-   site-bucket, list-only access to cloudlaunch-visible-only-bucket, and read-only permissions for VPC resources, with no delete rights
  Publicly accessible (read-only for anonymous users).

---


### Task 2: VPC Design for CloudLaunch Environment

- I created my VPC,
  VPC name: cloudlaunch-vpc
  CIDR Block: 10.0.0.0/16

 Subnets:

 Public: cloudlaunch-public-subnet – 10.0.1.0/24

 App (private): cloudlaunch-app-subnet – 10.0.2.0/24

 DB (private): cloudlaunch-db-subnet – 10.0.3.0/28

 Subnets Created

 ![Dubnets Created](./images/subnets%20created.png
IGW: cloudlaunch-igw (attached to cloudlaunch-vpc)

Route Tables:

cloudlaunch-public-rt → 0.0.0.0/0 via cloudlaunch-igw (associated to public subnet)

cloudlaunch-app-rt → no internet route (associated to app subnet)

cloudlaunch-db-rt → no internet route (associated to db subnet)
