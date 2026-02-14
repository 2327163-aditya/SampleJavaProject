pipeline{
    agent any
    environment{
        PATH = "/opt/maven/bin:$PATH"
    }
        stage('build'){
            steps{
                sh 'mvn clean install'
            }
        }
    }
}
