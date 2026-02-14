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
            environment {
                scannerHome = tool 'aditya-sonar-scanner'
            }
            steps {
                withSonarQubeEnv('aditya-sonarube-server') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
            }
        }

    }
}


