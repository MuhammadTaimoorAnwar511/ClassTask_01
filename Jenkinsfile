pipeline {
    agent any
    
    environment {
        DOCKER_USERNAME = 'taimooranwar'
        DOCKER_PASSWORD = 'Ta#1#2#3#4'
    }
    
    stages {
        stage('Checkout code') {
            steps {
                checkout scm
            }
        }
        
        stage('Set up Python') {
            steps {
                sh 'python --version || sudo apt-get install -y python3'
                sh 'python3 -m pip install --upgrade pip'
            }
        }

        stage('Install dependencies') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }
        
        stage('Build Docker image') {
            steps {
                sh 'docker build -t bitcoin-flask-app .'
            }
        }
        
        stage('Log in to Docker Hub') {
            steps {
                sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin'
            }
        }
        
        stage('Push Docker image to Docker Hub') {
            steps {
                sh 'docker tag bitcoin-flask-app $DOCKER_USERNAME/bitcoin-flask-app:latest'
                sh 'docker push $DOCKER_USERNAME/bitcoin-flask-app:latest'
            }
        }
    }
    
    post {
        always {
            echo 'Pipeline completed.'
        }
    }
}
