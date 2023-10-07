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

        // Add more stages for building, testing, and deploying your code
        stage('Build') {
            steps {
                'sh echo build'
            }
        }

        stage('Test') {
            steps {
                // Your testing steps go here
                sh 'echo test'
            }
        }

        stage('Deploy') {
            steps {
                // Your deployment steps go here

              sh 'echo deploy'
            }
        }
    }

    post {
        success {
            // Actions to perform when the pipeline is successful
        }
        failure {
            // Actions to perform when the pipeline fails
        }
    }
}

