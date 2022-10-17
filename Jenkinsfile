pipeline {
    agent any    
    stages{
        stage('Cloning Git') {
            steps {
            checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/kamaldogra/devops-pipeline']]])
            }
        }
        stage('Building Docker Image') {
            steps{
                script {
                bat "docker build -t kamaldogra87/devops-pipeline ."
                }
            }
        }
        stage('Pusing Image To Docker Hub') {
            steps{
                script {
                    withCredentials([string(credentialsId: 'dockerhub-cred', variable: 'dockerhubpwd')]) {
                        bat "docker login -u kamaldogra87 -p ${dockerhubpwd}"
                    }
                    bat "docker push kamaldogra87/devops-pipeline"
                }
            }
        }
        
    }
}