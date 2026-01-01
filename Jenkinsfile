pipeline {
    agent any
    
    tools {
        maven 'maven3.8.7'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/ejob12/maven-web-app.git'
            }
        }

        stage('Build Maven Project') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t ejob12/mavenwebapp .'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                withCredentials([file(credentialsId: 'eks-kubeconfig', variable: 'KUBECONFIG')]) {
                    // Verify cluster connectivity
                    sh 'kubectl --kubeconfig=$KUBECONFIG get nodes'
                    // Apply deployment manifest
                    sh 'kubectl --kubeconfig=$KUBECONFIG apply -f k8s-deploy.yml'
                }
            }
        }
    }
}
