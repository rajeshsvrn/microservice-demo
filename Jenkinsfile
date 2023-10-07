pipeline {
    agent any

    environment {
        // Define your Azure Container Registry name and resource group
        ACR_NAME = 'onlineboutiquedemo'
        IMAGE_TAG = '15'
        RESOURCE_GROUP = 'Online-Boutique'
        IMAGE_NAME = 'paymentservice'
        DOCKERFILE_PATH = './paymentservice/Dockerfile'
        AZURE_CRED = 'azure-cred'
        //ACR_ACCESS_KEY  = 'gf7ZAsys/bHm+1LEjg9ZHXHyTxyWztH5BinGq6ctI3+ACRAA9UXN'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from a Git repository
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/rajeshsvrn/microservice-demo.git']])
            }
        }
    

stage('Build and Push Docker Image') {
            steps {
                script {
                    withCredentials([string(credentialsId: 'ACR_ACCESS_KEY', variable: 'ACR_ACCESS_KEY')]) {
                sh """
                    docker login ${ACR_NAME}.azurecr.io -u ${ACR_NAME} -p \${ACR_ACCESS_KEY}
                """
            }

                // Build the Docker image
                    sh "docker build -t ${IMAGE_NAME}:${BUILD_NUMBER} -f ${DOCKERFILE_PATH} ."

                    // Tag the Docker image for ACR
                    sh "docker tag ${IMAGE_NAME}:${BUILD_NUMBER} ${ACR_NAME}.azurecr.io/${IMAGE_NAME}:${BUILD_NUMBER}"

                    // Push the Docker image to ACR
                    sh "docker push ${ACR_NAME}.azurecr.io/${IMAGE_NAME}:${BUILD_NUMBER}"
                        
                    }   
              }
            }     
     
        
    }  //Stages
}  //pipeline  
