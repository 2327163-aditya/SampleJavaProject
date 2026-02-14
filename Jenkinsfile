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
                // Ensure this matches the SonarQube server name exactly
                withSonarQubeEnv('aditya-sonarqube-server') {
                    // Use the scanner tool name exactly as configured in Global Tool Configuration
                    sh 'sonar-scanner'
                }
            }
        }

    }
}

