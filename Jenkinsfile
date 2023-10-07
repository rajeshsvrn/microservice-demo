pipeline {
    agent any

    environment {
        // Define your Azure Container Registry name and resource group
        ACR_NAME = 'onlineboutiquedemo'
        IMAGE_TAG = '15'
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
        
    stage('Authenticate with Azure') {
            steps {
                script {
                    withCredentials([azureServicePrincipal('azure-cred')]) {
                        // Use the Azure service principal credentials
                        sh """
                        az login --service-principal -u \$AZURE_CLIENT_ID -p \$AZURE_CLIENT_SECRET --tenant \$AZURE_TENANT_ID --allow-no-subscriptions
                        """
                    }
                }
            }
        }

stage('Build and Push Docker Image') {
            steps {
                script {
                    sh "pwd"
                    dir('/var/lib/docker/tmp/docker-builder1161398997/paymentservice') {
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
