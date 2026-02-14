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

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('aditya-sonarqube-server') {
                    sh 'mvn sonar:sonar'
                }
            }
        }

    }
}

