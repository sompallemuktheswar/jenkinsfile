pipeline {
    agent any

    stages {
        stage('checkout') {
            steps {
                git branch: 'main', url: 'git@github.com:sompallemuktheswar/jenkinsfile.git'
            }
        }
        stage('ECR login') {
            steps {
               sh "aws ecr get-login-password --region eu-west-3 | sudo docker login --username AWS --password-stdin 101275806917.dkr.ecr.eu-west-3.amazonaws.com" 
            }
        }
        stage('build image ') {
            steps {
               sh "sudo docker build -t 101275806917.dkr.ecr.eu-west-3.amazonaws.com/sunny:$BUILD_NUMBER . "
            }
        }
        stage('push image to ECR Repo') {
            steps {
              sh " sudo docker push 101275806917.dkr.ecr.eu-west-3.amazonaws.com/sunny:$BUILD_NUMBER"
            }
        }
        stage('deploy docker image as container inside jenkins instance') {
            steps {
              sh " sudo docker run -d -p 10000:80 101275806917.dkr.ecr.eu-west-3.amazonaws.com/sunny:$BUILD_NUMBER"
            }
        }
        stage('check docker containers') {
            steps {
              sh " sudo docker ps "
            }
        }
    }
}
