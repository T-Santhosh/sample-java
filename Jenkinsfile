pipeline {
    agent any

    environment {
        DOCKER_REPO = "your-docker-repo/demo"
        K8S_NAMESPACE = "default"
        K8S_DEPLOYMENT = "demo-deployment"
    }

    stages {
        stage('Build') {
            steps {
                script {
                    sh 'mvn clean package'
                }
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t $DOCKER_REPO:latest .'
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    sh 'docker push $DOCKER_REPO:latest'
                }
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                script {
                    sh 'kubectl apply -f deployment.yaml'
                }
            }
        }
    }
}
