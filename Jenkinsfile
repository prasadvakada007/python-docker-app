pipeline {
    agent any

    environment {
        IMAGE_NAME = "vakada007/hello-api"
        CONTAINER_NAME = "hello-api-container"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/prasadvakada007/python-docker-app.git'
            }
        }

        stage('Build & Push Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME:latest .'
                withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials',
                                                usernameVariable: 'DOCKER_USER',
                                                passwordVariable: 'DOCKER_PASS')]) {
                    sh '''
                        echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin
                        docker push $IMAGE_NAME:latest
                    '''
                }
            }
        }

        stage('Stop Previous Container') {
            steps {
                sh '''
                    docker stop $CONTAINER_NAME || true
                    docker rm $CONTAINER_NAME || true
                '''
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -d -p 5000:5000 --name $CONTAINER_NAME $IMAGE_NAME:latest'
            }
        }
    }
}
