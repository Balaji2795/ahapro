pipeline {
    agent any

    environment {
        IMAGE_NAME = "aha-html-app"
        CONTAINER_NAME = "aha-container"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t $IMAGE_NAME ."
                }
            }
        }

        stage('Stop Old Container') {
            steps {
                script {
                    sh "docker stop $CONTAINER_NAME || true"
                    sh "docker rm $CONTAINER_NAME || true"
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    sh "docker run -d -p 8080:80 --name $CONTAINER_NAME $IMAGE_NAME"
                }
            }
        }
    }
}
