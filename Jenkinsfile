pipeline {
    agent any;
    stages {
        stage('Build'){
            steps{
               sh "docker build -t tourly_image ."
            }
        }
        stage('Deploy'){
            steps{
                echo "hello Deploy World"
            }
        }
    }
}