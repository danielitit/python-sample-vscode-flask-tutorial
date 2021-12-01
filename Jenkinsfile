pipeline {
    environment {
        registry = "interacrdanny.azurecr.io/interview-python"
        registryCredential = 'azureacr'
        dockerImage = ''
    }
    agent any
    stages {
        stage('Sonarcloud - scan code') {
            steps {
                script {
                    def scannerHome = tool 'sonarscan';
                    withSonarQubeEnv('sonarqube') {
                        sh "${tool("sonarscan")}/bin/sonar-scanner -Dsonar.projectKey=danielitit_python-sample-vscode-flask-tutorial -Dsonar.projectName=python-sample-vscode-flask-tutorial"
                    }
                }
            }
        }
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
                    docker.withRegistry( 'https://interacrdanny.azurecr.io', registryCredential ) {
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