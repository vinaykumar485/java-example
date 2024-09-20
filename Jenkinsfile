pipeline {
    agent any
    stages {
        stage('Git Checkout') {
            steps {
                echo 'This is the Git Checkout stage'
                // Checkout your code if necessary (e.g., git checkout step)
            }
        }
        stage('Build') {
            steps {
                echo 'This is the Build stage'
                // Run Maven commands for building and SonarQube analysis
                sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=intigratioon -Dsonar.host.url=http://34.201.71.78:9000 -Dsonar.login=sqp_d77d4d2a6bf4d382026ac691191a060f83b4c0d6'
            }
        }
        stage('SonarQube Analysis') {
            steps {
                echo 'This is the SonarQube Analysis stage'
                // Additional SonarQube checks can be added here if necessary
            }
        }
        stage('Release') {
            steps {
                echo 'This is the Release stage'
                // Add steps related to releasing or deploying
            }
        }
    }
}
