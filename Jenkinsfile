pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/prasadvakada007/hello-api.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the Python app...'
                sh 'python3 --version'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'echo "Tests passed!"'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'
            }
        }
    }
}
