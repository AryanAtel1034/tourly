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
         stage('Push to ECR') {
            steps {
                sh '''
                AWS_REGION=ap-south-1
                ACCOUNT_ID=194477973016
                ECR_REPO=dev/mfe

                ECR_URL=194477973016.dkr.ecr.ap-south-1.amazonaws.com

                aws ecr get-login-password --region $AWS_REGION \
                | docker login --username AWS --password-stdin $ECR_URL

                docker build -t $ECR_REPO:latest .
                docker tag $ECR_REPO:latest $ECR_URL/$ECR_REPO:latest
                docker push $ECR_URL/$ECR_REPO:latest
                '''
            }
        }
        
    }
    post {
        always {
            archiveArtifacts artifacts: 'results.json', fingerprint: true
        }
    }
}
