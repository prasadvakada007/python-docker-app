pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/prasadvakada007/python-docker-app.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                python3 -m venv venv
                source venv/bin/activate
                pip install --upgrade pip
                pip install flask
                '''
            }
        }

        stage('Run App') {
            steps {
                sh '''
                source venv/bin/activate
                nohup python3 app.py &
                '''
            }
        }
    }
}
