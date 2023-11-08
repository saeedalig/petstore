#### Deploying a Java-based application called "Petstore" using a Continuous Integration/Continuous Deployment (CI/CD) pipeline with Jenkins and deploying it on a Kubernetes cluster. The goal is to automate the build, test, and deployment processes to ensure a streamlined and reliable deployment of the application.


## Server Setup (Installation)
- **AWS EC2 Instance:** t2.medium 
- **Jenkins**
```
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins -y

# Password
sudo cat /var/lib/jenkins/secrets/initialAdminPassword

```
