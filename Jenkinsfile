def registry = 'https://trial9a3imv.jfrog.io/'

pipeline {
    agent any

    environment {
        PATH = "/opt/maven/bin:${env.PATH}"
    }

    stages {

        stage('Build') {
            steps {
                sh 'mvn clean package -Dmaven.test.skip=true'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn surefire-report:report'
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

        stage("WAR Publish") {
            steps {
                script {
                    echo '<---------------- WAR Publish Started ----------------->'

                    def server = Artifactory.newServer(
                        url: registry + "artifactory",
                        credentialsId: "artifact-cred"
                    )

                    def properties = "buildid=${env.BUILD_ID};commitid=${GIT_COMMIT}"

                    def uploadSpec = """{
                        "files": [
                            {
                                "pattern": "target/*.war",
                                "target": "aditya-libs-release-local/",
                                "flat": "true",
                                "props": "${properties}",
                                "exclusions": ["*.sha1", "*.md5"]
                            }
                        ]
                    }"""

                    def buildInfo = server.upload(uploadSpec)
                    buildInfo.env.collect()
                    server.publishBuildInfo(buildInfo)

                    echo '<---------------- WAR Publish Ended ----------------->'
                }
            }
        }

    }
}

