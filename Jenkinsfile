pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from a Git repository
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/rajeshsvrn/microservice-demo.git']])
            }
        }
    }
}
