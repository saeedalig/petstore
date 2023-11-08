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

- **Docker**
```
sudo apt-get update
sudo apt-get install docker.io -y
sudo usermod -aG docker $USER   #my case is ubuntu
newgrp docker
sudo chmod 777 /var/run/docker.sock

```

- **Sonarqube**
```
docker run -d --name sonar -p 9000:9000 sonarqube:lts-community
```
You can access Sonarqube on port `9000`. Username and Password is same `admin`

- **Trivy**

```

sudo apt-get install wget apt-transport-https gnupg lsb-release -y
wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | gpg --dearmor | sudo tee /usr/share/keyrings/trivy.gpg > /dev/null
echo "deb [signed-by=/usr/share/keyrings/trivy.gpg] https://aquasecurity.github.io/trivy-repo/deb $(lsb_release -sc) main" | sudo tee -a /etc/apt/sources.list.d/trivy.list
sudo apt-get update
sudo apt-get install trivy -y

```

- **Ansible**
```

sudo apt update
sudo apt install software-properties-common
sudo add-apt-repository --yes --update ppa:ansible/ansible
sudo apt install ansible -y

```

- **Install Plugins like JDK, Sonarqube Scanner, Maven, OWASP Dependency Check, Docker, Ansible Kubernetes and others if required and configure them.**

