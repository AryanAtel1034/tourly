pipeline {
    agent any;
     environment {
        DOCKER_USER = 'aryanatel'
    }
    stages {
        stage('Docker Build'){
            steps{
               sh "docker build -t tourly_image ."
            }
        }
        stage('Docker Hub Login'){
            steps{
               withCredentials([string(credentialsId: 'docker_passwd', variable: 'docker_passwd')]) {
                sh "echo $docker_passwd | docker login -u $DOCKER_USER --password-stdin"
               }
            }
        }
         stage('Docker Push'){
            steps{
               sh "docker push aryanatel/tourly_image"
            }
        }
        stage('Docker Success Flag'){
            steps{
              echo "Docker push Login Successful"
            }
        }
        
    }
}