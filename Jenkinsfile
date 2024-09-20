pipeline {
    agent any
    stages {
        stage ('git checkout') {
            //agent {label 'slave-node'}
             steps {
                echo 'this is git checkout stage' 
            }
        }
        stage ('Build') {
            //agent {label 'slave-node'}
             steps {
                echo 'this is Build stage' 
            }
        }
        stage ('Sona Qube') {
            //agent {label 'slave-node'}
             steps {
                echo 'this is Sona Qube stage' 
            }
        }
        stage ('release') {
            //agent {label 'slave-node'}
            steps {
                echo 'this is release stage' 
            }
        }
    }
}	
