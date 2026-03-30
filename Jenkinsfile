pipeline {
    agent any;
     environment {
        DOCKER_USER = 'aryanatel'
    }
    stages {
        stage('Docker Build'){
            steps{
               sh "docker build -t aryanatel/tourly:$BUILD_NUMBER ."
            }
        }
        stage('Trivy FileSystem Scan'){
            steps{
               sh "trivy fs -f json -o results.json ."
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
               sh "docker push aryanatel/tourly:$BUILD_NUMBER"
            }
        }
        stage('Docker Success Flag'){
            steps{
              echo "Docker push Login Successful"
            }
        }
         stage('Webhook Success Flag'){
            steps{
              echo "wWebhook Successful $BUILD_NUMBER"
            }
        }
        
    }
}
