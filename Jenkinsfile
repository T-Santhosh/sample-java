pipeline {
    agent any

    environment {
        DOCKER_REPO = "your-docker-repo/demo"
        K8S_NAMESPACE = "default"
        K8S_DEPLOYMENT = "demo-deployment"
    }

    stages {
        stage ('git checkout'){
            steps{
                script{
                    git branch: 'main', url: 'https://github.com/T-Santhosh/sample-java.git'
                }
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
                    sh 'docker build -t santhosh2969/multi:v2 .'
                    sh 'docker images'
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    withCredentials([string(credentialsId: 'dockerPass', variable: 'dockerPassword')]) {
                        sh "docker login -u santhosh2969 -p ${dockerPassword}"
                        sh 'docker push santhosh2969/multi:v2'
                }
            }
        }
        }
        stage('Deploy to Kubernetes') {
            steps {
                script {
                     withKubeCredentials(kubectlCredentials: [[ credentialsId: 'kubernetes', namespace: 'ms' ]]) {
                        sh 'kubectl apply -f deployment.yaml'
                        sh 'kubectl get pods -o wide'
                }
            }
        }
    }
}
        
