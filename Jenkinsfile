pipeline {
    agent any
    stages {
        stage('Clone Code') {
            steps {
                git 'https://github.com/user/repo.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t myapp:latest .'
            }
        }
        stage('Push to Docker Hub') {
            steps {
                withDockerRegistry([credentialsId: 'docker-hub-cred', url: '']) {
                    sh 'docker tag myapp:latest user/myapp:latest'
                    sh 'docker push user/myapp:latest'
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
