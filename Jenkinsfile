pipeline {
    agent any
    
    tools{
        maven 'Maven-3.8.7'
    }
    stages {
        stage('clone') {
            steps {
              git 'https://github.com/ejob12/maven-web-app.git'
            }
        }
        stage('build'){
            steps{
                 sh 'mvn clean package'
            }
        }
        stage('docker image'){
            steps {
                sh 'docker build -t ejob12/mavenwebapp .'
            }
        }
        stage('k8s deploy'){
            steps{
               sh 'kubectl apply -f k8s-deploy.yml'
            }
        }
    }
}
