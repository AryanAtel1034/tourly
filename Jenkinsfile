pipeline {
    agent any;
     environment {
        DOCKER_USER = 'aryanatel'
    }
    stages {
        stage('Docker Build'){
            steps{
              echo "hello docker $BUILD_NUMBER"
            }
        }
       
        stage('Docker Success Flag'){
            steps{
              echo "Docker push Login Successful"
            }
        }
        
    }
}