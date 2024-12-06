# jenkins-pipeline
This repository contains an example Jenkins pipeline configuration (Jenkinsfile) to demonstrate Continuous Integration (CI) processes. The pipeline performs basic tasks such as building, testing, and deploying applications using Jenkins automation. It serves as a template for setting up CI/CD pipelines in Jenkins.


#**Prerequisites**:
Before installing Jenkins, make sure you meet the following prerequisites:

**AWS EC2 Instance:**
You should have an Ubuntu EC2 instance running (e.g., Ubuntu 20.04 LTS).
Security Group should allow access to ports 8080 (for Jenkins Web Interface) and 22 (for SSH).
**Access to EC2 Instance:**
You need an SSH private key (.pem file) to access the EC2 instance.
**Sudo Privileges:**
Ensure your EC2 user has sudo privileges to install packages.

**Step-by-Step Guide to Install Jenkins on EC2 Instance:**

**Java (JDK)**
Run the below commands to install Java and Jenkins
**Install Java**

sudo apt update
sudo apt install openjdk-17-jre

**Verify Java is Installed**

java -version

Now, you can proceed with installing Jenkins

curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins

**Note: ** By default, Jenkins will not be accessible to the external world due to the inbound traffic restriction by AWS. Open port 8080 in the inbound traffic rules as show below.

EC2 > Instances > Click on
In the bottom tabs -> Click on Security
Security groups
Add inbound traffic rules as shown in the image (you can just allow TCP 8080 as well, in my case, I allowed All traffic).
![Security group](https://github.com/user-attachments/assets/08c52b01-2f33-4e4b-a2a0-d3dfedae7ad6)

Login to Jenkins using the below URL:
http://:8080 [You can get the ec2-instance-public-ip-address from your AWS EC2 console page]

Note: If you are not interested in allowing All Traffic to your EC2 instance 1. Delete the inbound traffic rule for your instance 2. Edit the inbound traffic rule to only allow custom TCP port 8080

After you login to Jenkins, - Run the command to copy the Jenkins Admin Password - sudo cat /var/lib/jenkins/secrets/initialAdminPassword - Enter the Administrator password
<img width="1291" alt="Getting Started" src="https://github.com/user-attachments/assets/fe34a285-8dcd-4f01-89d8-fa63ee9bb215">

Click on Install suggested plugins
<img width="1291" alt="Getting Started-02" src="https://github.com/user-attachments/assets/11efba8d-bb12-4a74-a16c-8eecaeb73edb">

Wait for the Jenkins to Install suggested plugins
<img width="1291" alt="Getting Started-03" src="https://github.com/user-attachments/assets/767bf1f3-cbc6-4565-a779-b3d3a0b50368">

Create First Admin User or Skip the step [If you want to use this Jenkins instance for future use-cases as well, better to create admin user]

Jenkins Installation is Successful. You can now starting using the Jenkins

<img width="990" alt="Jenkins is Ready" src="https://github.com/user-attachments/assets/e7d984c5-114d-41e4-86f0-d8f9a0e6ba97">

