pipeline {
    agent any
    tools{
        maven 'M2_HOME'
    }
    environment {
    registry = '561422302125.dkr.ecr.us-east-1.amazonaws.com/devops_repo'
    registryCredential = 'jenkins-ecr'
    dockerimage = ''
  }
    stages {
        stage('Checkout'){
            steps{
                git branch: 'main', url: 'https://github.com/deboadigun/geolocation.git'
            }
        }
        stage('Code Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Build Image') {
            steps {
                script{
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                } 
            }
        }
        stage('Deploy image') {
            steps{
                script{ 
                    docker.withRegistry("https://561422302125.dkr.ecr.us-east-1.amazonaws.com/devops_repo","ecr:us-east-1:jenkins-ecr") {
                        dockerImage.push()
                    }
                }
            }
        }  
    }
}