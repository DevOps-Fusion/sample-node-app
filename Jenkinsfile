pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials')
        IMAGE_NAME = "prabhat2025/sample-node-app"
        BUILD_TAG = "${BUILD_NUMBER}" 
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/DevOps-Fusion/sample-node-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME:$BUILD_TAG .'
                sh 'docker tag $IMAGE_NAME:$BUILD_TAG $IMAGE_NAME:latest'
            }
        }

        stage('Login to Docker Hub') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }

        stage('Push Docker Image') {
            steps {
                sh 'docker push $IMAGE_NAME:$BUILD_TAG'
                sh 'docker push $IMAGE_NAME:latest'
            }
        }
    }
}
