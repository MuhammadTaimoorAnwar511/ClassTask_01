pipeline {
    agent any

    environment {
        DOCKER_USERNAME = 'taimooranwar'
        DOCKER_PASSWORD = 'Ta#1#2#3#4'
    }

    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Set up Python Virtual Environment') {
            steps {
                sh '''
                python3 -m venv venv
                source venv/bin/activate
                python3 -m pip install --upgrade pip
                pip install -r requirements.txt
                '''
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t bitcoin-flask-app .'
            }
        }

        stage('Docker Login') {
            steps {
                sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin'
            }
        }

        stage('Push Docker Image') {
            steps {
                sh 'docker tag bitcoin-flask-app $DOCKER_USERNAME/bitcoin-flask-app:latest'
                sh 'docker push $DOCKER_USERNAME/bitcoin-flask-app:latest'
            }
        }
    }
}
