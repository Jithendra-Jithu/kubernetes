pipeline {
    agent any
    environment {
        DOCKER_IMAGE = 'jithu145/kubernetes:latest'
        K8S_DEPLOYMENT_FILE = 'k8s-deployment.yaml'
        REGISTRY_CREDENTIALS = 'docker-creds'  // Docker Hub credentials stored in Jenkins
        K8S_CREDENTIALS = 'kubeconfig-creds'  // Kubernetes credentials stored in Jenkins
    }
    stages {
        stage('Clone Code') {
            steps {
                // Clone the repository
                git 'https://github.com/Jithendra-Jithu/kubernetes.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                // Build Docker image
                script {
                    sh 'docker build -t ${DOCKER_IMAGE} .'
                }
            }
        }

        stage('Push Docker Image to Docker Hub') {
            steps {
                // Login to Docker Hub and push the Docker image
                withDockerRegistry([credentialsId: REGISTRY_CREDENTIALS]) {
                    sh 'docker push ${DOCKER_IMAGE}'
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                // Apply the Kubernetes deployment
                withCredentials([file(credentialsId: K8S_CREDENTIALS, variable: 'KUBECONFIG')]) {
                    sh "kubectl apply -f ${K8S_DEPLOYMENT_FILE}"
                }
            }
        }
    }
    post {
        success {
            echo 'CI/CD Pipeline completed successfully!'
        }
        failure {
            echo 'CI/CD Pipeline failed!'
        }
    }
}
