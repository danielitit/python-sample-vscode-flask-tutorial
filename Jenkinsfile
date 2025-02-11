pipeline {
    environment {
        registry = "interacrdanny.azurecr.io/interview-python"
        registryCredential = 'azureacr'
        dockerImage = ''
        scannerHome = tool name: 'sonarscanner'
    }
    agent any
    stages {
        stage('Sonarcloud - scan code') {
            steps {
                script {
                    withSonarQubeEnv('SonarQube') {
                        sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=interview -Dsonar.sources=. -Dsonar.host.url=http://20.93.31.185:9000 -Dsonar.login=1a484c8c344291efcb5168fae2d4b70ed2847cd5"
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
        stage('Deploy to PROD') {
            options {
                timeout(time: 30, unit: 'SECONDS') 
            }
            input {
                message "Should we continue?"
            }
            steps {
                echo "Helm deploy"
            }
        }
    }
    post { 
        always { 
            echo 'I will always say Hello again!'
        }
    }
}