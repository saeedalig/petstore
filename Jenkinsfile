pipeline{
    agent any
    tools{
        jdk 'jdk17'
        maven 'maven3'
    }
	
    environment {
        SCANNER_HOME=tool 'sonar-scanner'
    }
	
    stages {
	
        stage('Clean Workspace'){
            steps{
                cleanWs()
            }
        }
		
        stage('Git Checkout'){
            steps{
                git branch: 'main', url: 'https://github.com/saeedalig/petstore.git'
            }
        }
		
		stage ('MVN Compile') {
            steps {
                sh 'mvn clean compile'
            }
        }
		
        stage ('MVN Test') {
            steps {
                sh 'mvn test'
            }
        }
		
        stage('Sonarqube Code Analysis'){
            steps{
                withSonarQubeEnv('sonar-server') {
                    sh ''' $SCANNER_HOME/bin/sonar-scanner \
					-Dsonar.projectName=Petstore \
                    -Dsonar.projectKey=Petstore'''
                }
            }
        }
		
        stage('Quality Gate Status'){
           steps {
                script {
                    waitForQualityGate abortPipeline: false, credentialsId: 'sonar-token' 
                }
            } 
        }

	stage ('Build War File'){
            steps{
                sh 'mvn clean install -DskipTests=true'
            }
        }

        stage('OWASP FS SCAN') {
            steps {
                dependencyCheck additionalArguments: '--scan ./ --disableYarnAudit --disableNodeAudit', odcInstallation: 'DP-Check'
                dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
            }
        }
		
        stage('Scan Files: TRIVY') {
            steps {
                sh "trivy fs . > trivy-fs.txt"
            }
        }
		
        stage ("Docker Build & Tag") {
            steps {
                dir('ansible-plays'){
					script {
						ansiblePlaybook credentialsId: 'ssh', 
						disableHostKeyChecking: true, 
						installation: 'ansible', 
						inventory: '/etc/ansible/', 
						playbook: 'docker.yaml'
					}
				}
            }
        }
		
	stage('k8s deployment using Ansible'){
            steps{
                dir('ansible-plays'){
                    script{
                        ansiblePlaybook credentialsId: 'ssh', 
						disableHostKeyChecking: true, 
						installation: 'ansible', 
						inventory: '/etc/ansible/', 
						playbook: 'kubernetes.yaml'
                    }
                } 
            }
        }	
   }
}
