pipeline {
    agent any

    stages {
        stage('checkout') {
            steps {
               git branch: 'main', url: 'git@github.com:sompallemuktheswar/jenkinsfile.git'
            }
        }
         stage('login') {
            steps {
               sh "aws ecr get-login-password --region eu-west-3 | docker login --username AWS --password-stdin 101275806917  
               }
        stage('build ') {
            steps {
               sh "docker tag sunny:latest 101275806917.dkr.ecr.eu-west-3.amazonaws.com/sunny:latest ."
            }
        }
        stage('push') {
            steps {
               sh " docker push 101275806917.dkr.ecr.eu-west-3.amazonaws.com/sunny:latest"
        }

    }
    
}
