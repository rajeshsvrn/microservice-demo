pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from a Git repository
                checkout([$class: 'GitSCM',
                          branches: [[name: 'main']], // Specify the branch you want to check out
                          userRemoteConfigs: [[url: 'https://github.com/rajeshsvrn/microservice-demo.git']]])
            }
        }
    }
