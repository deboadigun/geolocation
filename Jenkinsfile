pipeline {
    agent any

    tools {
  maven 'M2_HOME'
}

    triggers {
  pollSCM ('* * * * *')
}

    stages {
        stage('maven package') {
            steps {
                sh 'mvn clean'
                sh 'mvn install'
                sh 'mvn package'

                sleep 2
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'

                sleep 2
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploy Steps'

                sleep 2
            }
        }

        stage('Docker') {
            steps {
                echo 'Image Steps'

                sleep 2
            }
        }
    }
}