pipeline {
    agent any

    environment {
        // Define your Azure Container Registry name and resource group
        ACR_NAME = 'onlineboutiquedemo'
        RESOURCE_GROUP = 'Online-Boutique'
        IMAGE_NAME = 'paymentservice'
        DOCKERFILE_PATH = './paymentservice'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from a Git repository
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/rajeshsvrn/microservice-demo.git']])
            }
        }

        stage('build image and publish'){
            steps{
                    script {
                    // Login to Azure using service principal credentials
                    withCredentials([azureServicePrincipal('azure-cred')]) {
                        sh "az acr login --name ${ACR_NAME}"
                        
                        // Build the Docker image
                        sh "docker build -t ${IMAGE_NAME}:${BUILD_NUMBER} -f ${DOCKERFILE_PATH} ."
                        
                        // Tag the Docker image for ACR
                        sh "docker tag ${IMAGE_NAME}:${BUILD_NUMBER} ${ACR_NAME}.azurecr.io/${IMAGE_NAME}:${BUILD_NUMBER}"
                        
                        // Push the Docker image to ACR
                        sh "docker push ${ACR_NAME}.azurecr.io/${IMAGE_NAME}:${BUILD_NUMBER}"
                    }
                }       
            }
        }  
        
        
    }  //Stages
}  //pipeline  
