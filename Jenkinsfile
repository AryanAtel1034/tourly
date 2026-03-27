pipeline {
    agent any;
     environment {
        DOCKER_USER = 'your-docker-username'
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
                sh "docker login -u $DOCKER_USER -p $docker_passwd"
               }
            }
        }
        stage('Docker Hub Flag'){
            steps{
              echo "Docker Hub Login Successful"
            }
        }
        
    }
}