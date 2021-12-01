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
                    docker.Image = docker.build registry + ":$BUILD_NUMBER"
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