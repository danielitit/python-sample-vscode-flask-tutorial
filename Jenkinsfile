pipeline {
    environment {
        registry = "interacrdanny.azurecr.io/interview-python"
        registryCredential = 'azureacr'
        dockerImage = ''
    }
    agent any
    stages {
        stage('Build docker image') {
            steps {
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
        stage('Push docker image') {
            steps {
                script {
                    docker.withRegistry( 'interacrdanny.azurecr.io', registryCredential ) {
                        dockerImage.push()
                    }
                }
            }
        }
    }
    post { 
        always { 
            echo 'I will always say Hello again!'
        }
    }
}