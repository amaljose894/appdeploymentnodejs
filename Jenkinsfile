pipeline {
    agent any
    environment {
      TAG = getDockertag()
    }
    stages {
        stage('Source Code CheckOut') {
           
            steps {
                echo 'Pulling Latest Infra Code From bit Bucket'
              git([url: 'https://arjunavofficial@bitbucket.org/arjunavofficial/applicationdeployment_nodejs.git', branch: 'master'])
            
                
            }
        }
        stage('Building and Pushing Image to Artifactory') {
           
            steps {
            echo "1"
            sh 'docker login -u="amaljose" -p="jVbExP0/l2geeWxzbTqiAsbxqwd9UM00r20DAj83newLLuXrZmxWDmrVYuYfAQ3n" quay.io'
            sh 'TAG=`git rev-parse --short HEAD`'
            sh 'docker build -t quay.io/amaljose/nodejs:${TAG} .'
            sh 'docker image push quay.io/amaljose/nodejs:${TAG}'
            }
        }
            stage('Deploying Application') {
           
            steps {
            echo "2"
            sh 'sudo ansible-playbook  --extra-vars "TAG=${TAG}" deploy_nodejs.yml'
                }
            }
    
    } 
}

def  getDockertag(){
    def tag = sh script: 'git rev-parse --short HEAD' , returnStdout: true
    return tag
}


