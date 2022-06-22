pipeline {
    agent any 
    environment {
        registryCredential = 'dockerhub'
        imageName = 'salam9920/nodejsapp'
        dockerImage = ''
        }
    stages {
        stage('Run the tests') {
             agent {
                any { 
                    image 'node:18-alpine'
                    args '-e HOME=/tmp -e NPM_CONFIG_PREFIX=/tmp/.npm'
                    reuseNode true
                }
            }
            steps {
                echo 'Retrieve source from github. run npm install and npm test' 
            }
        }
        stage('Building image') {
            steps{
                script {
                    echo 'build the image' 
                }
            }
            }
        stage('Push Image') {
            steps{
                script {
                    echo 'push the image to docker hub' 
                }
            }
        }     
         stage('deploy to k8s') {
             agent {
                any { 
                    image 'google/cloud-sdk:latest'
                    args '-e HOME=/tmp'
                    reuseNode true
                        }
                    }
            steps {
                script {
                    echo 'do nothing here' 
                 // echo 'do nothing here'
                 //echo 'do nothing here'
                }
        }     
        stage('Remove local docker image') {
            steps{
                sh "docker rmi $imageName:latest"
                sh "docker rmi $imageName:$BUILD_NUMBER"
            }
        }
    }
