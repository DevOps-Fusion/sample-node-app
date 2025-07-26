pipeline {
    agent any

    tools {
        nodejs "NodeJS" // This must match the name set in Jenkins Global Tool Configuration
    }

    environment {
        IMAGE_NAME = "sample-node-app"
    }

    stages {
        stage('Clone') {
            steps {
                // Cloning is handled by Jenkins automatically when using Pipeline from SCM
                echo "Source code already cloned by Jenkins from https://github.com/DevOps-Fusion/sample-node-app.git"
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test'
            }
        }

        stage('Docker Build') {
            steps {
                script {
                    docker.build("${env.IMAGE_NAME}")
                }
            }
        }
    }
}
