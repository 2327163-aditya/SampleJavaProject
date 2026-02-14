pipeline {
    agent any

    environment {
        PATH = "/opt/maven/bin:${env.PATH}"
    }

    stages {

        stage('Build & Test') {
            steps {
                sh 'mvn clean verify'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('aditya-sonarqube-server') {
                    sh """
                    mvn sonar:sonar \
                    -Dsonar.organization=2327163-aditya \
                    -Dsonar.projectKey=2327163-aditya \
                    -Dsonar.host.url=https://sonarcloud.io
                    """
                }
            }
        }

    }
}

