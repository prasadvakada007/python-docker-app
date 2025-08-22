pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/prasadvakada007/hello-api.git'
            }
        }

        stage('Install dependencies') {
            steps {
                sh 'python3 -m venv venv'
                sh './venv/bin/pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'echo "Running tests..."'
                // You can add pytest or unittest here if available
            }
        }

        stage('Run Application') {
            steps {
                sh './venv/bin/python app.py &'
            }
        }
    }
}
