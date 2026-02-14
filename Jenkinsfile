pipeline {
    agent any

    environment {
        MAVEN_HOME = tool name: 'Maven-3.9.0', type: 'maven'
        PATH = "${MAVEN_HOME}/bin:${env.PATH}"
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

