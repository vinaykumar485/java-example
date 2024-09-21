pipeline {
    agent any

    environment {
        // Define your environment variables for tools and credentials
        SONARQUBE_SERVER = 'SonarQube'                                            // SonarQube server configured in Jenkins
        SONARQUBE_TOKEN = 'sqp_06378a1a92b28504e8b563e99a0a7710616d7e9f'            // Credentials ID for SonarQube token
        ARTIFACTORY_URL = 'http://107.23.185.82:8081'
        ARTIFACTORY_CREDENTIALS = 'winay@8061'                                   // Credentials ID for Artifactory
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', https://github.com/vinaykumar485/java-example.git'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh """
                        mvn clean verify sonar:sonar 
  				-Dsonar.projectKey=sonarquneproject 
 				-Dsonar.host.url=http://34.235.127.234:9000 
  				-Dsonar.login=sqp_06378a1a92b28504e8b563e99a0a7710616d7e9f}
                    """
                }
            }
        }

        stage('Build') {
            steps {
                // Execute a Maven build (adjust according to your build tool)
                sh 'mvn clean install'
            }
        }

        stage('Upload Artifact to Artifactory') {
            steps {
                script {
                    def server = Artifactory.server 'Artifactory'
                    def buildInfo = server.upload spec: """{
                        "files": [{
                            "pattern": "target/*.war",  // Path to your artifact (JAR, WAR, etc.)
                            "target": "jfrogkey-2/"
                        }]
                    }"""
                    server.publishBuildInfo buildInfo
                }
            }
        }

        stage('Quality Gate') {
            steps {
                script {
                    // Wait for SonarQube to finish and check the Quality Gate status
                    timeout(time: 5, unit: 'MINUTES') {
                        def qualityGate = waitForQualityGate()
                        if (qualityGate.status != 'OK') {
                            error "Pipeline aborted due to quality gate failure: ${qualityGate.status}"
                        }
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline succeeded!'
        }

        failure {
            echo 'Pipeline failed!'
        }

        always {
            cleanWs()  // Clean the workspace after the pipeline execution
        }
    }
}
