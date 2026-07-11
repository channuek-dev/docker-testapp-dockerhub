pipeline {
    agent any

    environment {
        IMAGE_NAME = "chhanaek/docker-testapp-dockerhub:latest"
        DOCKER_BUILDKIT = "0"
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm ci'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %IMAGE_NAME% .'
            }
        }

        stage('Docker Login') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub-credentials',
                        usernameVariable: 'DOCKER_USER',
                        passwordVariable: 'DOCKER_PASS'
                    )
                ]) {
                    bat '''
                    @echo off
                    echo %DOCKER_PASS%| docker login -u %DOCKER_USER% --password-stdin
                    '''
                }
            }
        }

        stage('Push Image') {
            steps {
                bat '''
                docker push %IMAGE_NAME%
                exit /b 0
                '''
            }
        }
    }

    post {
        always {
            bat 'docker logout'
        }
    }
}