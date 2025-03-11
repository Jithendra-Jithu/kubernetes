pipeline {
    agent any
    stages {
        stage('Clone Code') {
            steps {
                git 'https://github.com/Jithendra-Jithu/kubernetes.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t jithu145/kubernetes:latest .'
            }
        }
        stage('Push to Docker Hub') {
            steps {
                withDockerRegistry([credentialsId: 'docker-creds', url: '']) {
                    sh 'docker push jithu145/kubernetes:latest'
                }
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f k8s-deployment.yaml'
            }
        }
    }
}
