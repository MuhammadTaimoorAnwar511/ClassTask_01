pipeline {
    agent any
    environment {
        DOCKER_USERNAME = 'taimooranwar'
        DOCKER_PASSWORD = 'Ta#1#2#3#4'
    }
    stages {
        stage('Checkout code') {
            steps {
                git branch: 'master', url: 'https://your-repo-url.git'
            }
        }
        stage('Set up Python') {
            steps {
                sh 'python3 -m pip install --upgrade pip'
            }
        }
        stage('Install dependencies') {
            steps {
                sh 'pip3 install -r requirements.txt'
            }
        }
        stage('Build Docker image') {
            steps {
                sh 'docker build -t bitcoin-flask-app .'
            }
        }
        stage('Login to Docker Hub') {
            steps {
                script {
                    sh "echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin"
                }
            }
        }
        stage('Push Docker image to Docker Hub') {
            steps {
                script {
                    sh "docker tag bitcoin-flask-app ${DOCKER_USERNAME}/bitcoin-flask-app:latest"
                    sh "docker push ${DOCKER_USERNAME}/bitcoin-flask-app:latest"
                }
            }
        }
    }
}
