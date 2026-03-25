pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "your-dockerhub-username/aha-app"
        TAG = "latest"
    }

    stages {

        stage('Clone Repo') {
            steps {
                git 'https://github.com/your-repo/aha-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE:$TAG .'
            }
        }

        stage('Login to Docker Hub') {
            steps {
                withCredentials([string(credentialsId: 'dockerhub-password', variable: 'PASS')]) {
                    sh 'echo $PASS | docker login -u your-dockerhub-username --password-stdin'
                }
            }
        }

        stage('Push Image') {
            steps {
                sh 'docker push $DOCKER_IMAGE:$TAG'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f k8s-deployment.yaml'
                sh 'kubectl apply -f k8s-service.yaml'
            }
        }
    }
}
