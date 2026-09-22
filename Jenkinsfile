pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out source code...'
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                bat 'docker build -t ai-devops-app:1.0 .'
            }
        }

        stage('Start Minikube') {
            steps {
                echo 'Checking Minikube cluster...'
                bat 'minikube status'
            }
        }

        stage('Load Image into Minikube') {
            steps {
                echo 'Loading Docker image into Minikube...'
                bat 'minikube image load ai-devops-app:1.0'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                echo 'Deploying application to Kubernetes...'
                bat 'kubectl apply -f k8s\\deployment.yaml'
                bat 'kubectl apply -f k8s\\service.yaml'
            }
        }

        stage('Verify Deployment') {
            steps {
                echo 'Checking Kubernetes deployment...'
                bat 'kubectl get pods'
                bat 'kubectl get services'
            }
        }
    }

    post {
        success {
            echo 'CI/CD pipeline completed successfully!'
        }

        failure {
            echo 'CI/CD pipeline failed.'
        }
    }
}