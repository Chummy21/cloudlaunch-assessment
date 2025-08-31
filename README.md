### NAME: Sylvia Chioma Okafor

### ALTSCHOOL ID: ALT/SOE/024/4939

## Cloudlaunch-Assessment
This repository contains my implementation of CloudLaunch, a project demonstrating core AWS skills. The project covers:

Static Website Hosting on S3 – Hosting a public website securely with read-only access for anonymous users, private storage for sensitive documents, and a visible-but-restricted bucket.

📌 IAM User Management – A custom IAM user with limited, precise permissions for secure access control across the three S3 buckets.

📌 VPC Design – A logically separated VPC with public, app, and database subnets, internet gateway, route tables, and security groups to demonstrate secure network architecture.

📌 All resources are created within the AWS Free Tier and follow best practices for access control and network segmentation.

## Task 1: Static Website on S3 + IAM

- **Buckets created**:
  - `cloudlaunch-site-bucketchioma` (public read for website)
  - `cloudlaunch-private-bucketchioma` (private; IAM user Get/Put only; no Delete)
  - `cloudlaunch-visible-only-bucketchioma` (listable by IAM user; contents not accessible)

- **Website link**:
  - S3 website endpoint: [s3-website-endpoint](http://cloudlaunch-site-bucketchioma.s3-website-eu-west-1.amazonaws.com)
  - **Bonus (if used)**: CloudFront URL: `https://<your-distribution-id>.cloudfront.net`
 
  - [https://chummy7.strangled.net](https://chummy7.strangled.net)


- **IAM user**: `cloudlaunch-user`
  - Console sign-in URL: `https://<your-account-id-or-alias>.signin.aws.amazon.com/console`
  - Username: `cloudlaunch-user`
  - Temporary password: `<provide temp password>` (password reset enforced on first login)

> ⚠️ Security note: This user is highly restricted and created only for grading. After grading, the user will be **deleted**.

- **IAM policy JSON** (attached to `cloudlaunch-user`):

```json
<paste the exact policy from the guide here>




---

## 📌 Project Description

This project showcases a responsive cloud-themed landing page, deployed on an AWS EC2 instance with Nginx as the web server. It was developed as part of my 
AltSchool Africa Tinyuka Second Semester coursework, where I explored the core principles of Linux server provisioning, static site deployment, and web server 
configuration in a real-world cloud environment.



## 🔗 Live Demo

- **Public IP**: [http:/18.175.140.50](http://18.175.140.50)  
- **Secure HTTPS**: [https://chummy7.strangled.net](https://chummy7.strangled.net)

---


## 🗂️ Project Structure

cloud-landing-page/
├── index.html
├── assets
├── README.md

## 📌Project Features

- Responsive HTML/CSS landing page
- Tailwind CSS for styling via CDN
- Hosted on AWS EC2 Ubuntu server
- Nginx web server for deployment
- Git + GitHub for version control
- FreeDNS subdomain mapping (optional)
- SSL via Let’s Encrypt (Certbot)


## 🚀 Steps Taken to complete the project

### 1. 🖊️ Created the Web Page and tested it

- I created the following files:

- index.html
This file contains the structure and content of my landing page. Tailwind CSS was integrated via CDN for responsive styling. I also embedded a small JavaScript function to enhance the page experience dynamically during refresh.

- style.css (Optional)
Although Tailwind handled most styling, I used this CSS file for any additional custom styles or animations that Tailwind didn’t cover directly.

- README.md
A detailed markdown file documenting the project structure, setup process, deployment steps, challenges faced, and screenshots of the live deployment.

- assets/ (Also called the images folder/)
This folder holds all image assets used in the landing page, including screenshots of the EC2 setup, Nginx installation, SSL certification, Git clone, and the rendered webpage in a browser.

- After completing the design and tests locally, I initialized a Git repository and pushed all the project files to GitHub.

- These files were later cloned into my EC2 instance during the deployment process, where I served the webpage using Nginx and configured HTTPS using Certbot.


### 2. **EC2 Instance Setup**  

- To host my landing page, I provisioned an EC2 instance using AWS with the following configuration:

- I already had an AWS account, thus, to host my landing page, I had to provision an EC2 instance using AWS. So, I logged into the AWS Management Console and searched for EC2 in the top search bar. From the EC2 dashboard, I clicked on “Launch Instance” to begin provisioning my virtual server.

  I followed these steps during the setup:

- Gave the instance a name (CloudLandingPage). 

- Selected the Ubuntu Server 22.04 LTS (64-bit) as my preferred AMI.

- Choose the t2.micro instance type, which is eligible for the AWS Free Tier.

- Created a new key pair for SSH access (though I later used EC2 Instance Connect for convenience).

- Configured the network settings by allowing the security group rules:

   SSH (port 22) – to connect to the server

   HTTP (port 80) – to serve the webpage

   HTTPS (port 443) – to enable SSL/TLS

- Allocated 8 GB of general-purpose SSD storage.

- Reviewed the settings and launched the instance.

Once the instance was running, I connected to it using EC2 Instance Connect. This gave me terminal access where I could install and configure Git and Nginx within the server. I was also able to pull my code from GitHub and set up the environment for deploying the landing page.

   ![HTTPS Enabled](./assets/Security%20Group.png)  

   - EC2 Instance Created
   ![EC2 Instance](./assets/EC2%20instance%20created.png)
   
### 3. **Connecting to EC2, Installing Nginx and Cloning the GitHub Repository**  
   After gaining access to my EC2 instance via EC2 Instance Connect, I proceeded to set up the web server environment and deploy my landing page.
   First, I accessed the instance via SSH and installed Nginx.  

   - I updated the system packages to ensure the server had the latest software:
   - ![sudo apt update](./assets/sudo%20apt%20updates.png) 
   - **Before Nginx Installation**:  
     ![Before Nginx](./assets/Before%20Installing%20nginx.png)

   - Nginx Installation
     
   -  ![nginx](./assets/nginx.png)
     
   - **After Nginx Installation**:  
     ![After Nginx](./assets/After%20installing%20nginx.png)

### 4. Cloned the GitHub Repo on EC2 Using:
 - git clone https://github.com/Chummy21/cloud-landing-page.git
 - ![Git Clone](./assets/git-clone-ec2.png)


### 5. **Deploying the Web Page**  
   - Replaced the default Nginx HTML file with my custom HTML file.  
   - ![Deployed Web Page](./assets/Custom%20HTML%20File.png)

   
### 6. **Subdomain Creation with FreeDNS**  
  - Created a subdomain using FreeDNS.
  - Pointed it to my EC2 Public IP.
  - Verified using ping and browser
   ![Subdomain Creation](./assets/subdomain%20creation.png)


### 7. **Securing the Subdomain with Certbot** 🛡️ 
   - **After SSL Installation**:
   - This is the *rendered page*
     ![After SSL](./assets/After%20SSL.png)


---

### 8. **Submission/Deliverables** 🛡️

Domain name: chummy7.strangled.net

Public IP Address: 18.175.140.50

Public URL Address: https://chummy7.strangled.net/

---

## ⚠️ Problems Encountered

- Initially encountered issues installing Tailwind CSS locally, so I opted to use the official CDN instead.
- Experienced network-related delays while attempting to host the site.
- Accidentally reused the same email address during SSL certification, which resulted in rate-limit delays.
- Faced challenges pushing files via HTTPS, so I switched to using SSH for version control.
- Exceeded Let's Encrypt’s certificate request limits for the same domain, which delayed the SSL installation. I had to switch to a different subdomain to proceed.


---

PS:This site may not be available after 4 weeks, as I plan to shut down the EC2 instance to avoid unexpected charges on my AWS account.
---

If you have any questions, feedback, or suggestions, feel free to reach out or connect with me directly. I would love to hear from you!

📧 Email: chiomagerald@gmail.com
🔗 LinkedIn: [Okafor Chioma](https://www.linkedin.com/in/okafor-chioma/)

---

## 🙏 Acknowledgement

I’m deeply thankful to God for the accomplishment of this project and for the chance to grow as a student at AltSchool. My heartfelt appreciation goes to my Instructor who imparted the knowledge, and finally, my husband and family whose constant encouragement and support made this journey possible.


---
