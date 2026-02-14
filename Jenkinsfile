pipeline {
    agent any

    environment {
        PATH = "/opt/maven/bin:${env.PATH}"
    }

    stages {

        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('SonarQube analysis') {
            steps {
                // Use the exact name of your SonarQube installation in Jenkins
                withSonarQubeEnv('aditya-sonarube-server') {
                    // Call sonar scanner using the Jenkins tool configuration
                    sh 'sonar-scanner'
                }
            }
        }

    }
}

