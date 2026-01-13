pipeline {
    agent any

    tools {
        maven 'M2_HOME'
    }

    stages {

        stage('Clone repo') {
            steps {
                git 'https://github.com/zuber383/jenkins-project-8.git'
            }
        }

        stage('Compile Code') {
            steps {
                bat 'mvn compile'
            }
        }

        stage('Test Code') {
            steps {
                bat 'mvn test'
            }
            post {
                success {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }

        stage('Package Code') {
            steps {
                bat 'mvn package'
            }
        }

    }
}
