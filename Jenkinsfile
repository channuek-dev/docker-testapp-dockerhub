pipeline {

    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install') {
            steps {
                bat 'npm ci'
            }
        }

        stage('Verify Syntax') {
            steps {
                bat 'node --check server.js'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t docker-testapp:latest .'
            }
        }

        stage('List Docker Images') {
            steps {
                bat 'docker images'
            }
        }
    }

    post {
        success {
            echo 'Build completed successfully.'
        }
        failure {
            echo 'Build failed.'
        }
    }
}