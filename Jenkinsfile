pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Verify Application') {
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
            echo 'Pipeline completed successfully!'
        }

        failure {
            echo 'Pipeline failed.'
        }
    }
}