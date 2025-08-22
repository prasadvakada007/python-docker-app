pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials')
        IMAGE_NAME = "prasadvakada007/hello-api"
        IMAGE_TAG = "latest"
        CONTAINER_NAME = "hello-api-container"
        APP_PORT = "5000"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/prasadvakada007/python-docker-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t $IMAGE_NAME:$IMAGE_TAG ."
            }
        }

        stage('Docker Login') {
            steps {
                sh "echo Prasad@123 | docker login -u prasadvakada007 --password-stdin"
            }
        }

        stage('Push to Docker Hub') {
            steps {
                sh "docker push $IMAGE_NAME:$IMAGE_TAG"
            }
        }

        stage('Stop Previous Container') {
            steps {
                sh """
                if [ \$(docker ps -q -f name=$CONTAINER_NAME) ]; then
                    docker stop $CONTAINER_NAME
                    docker rm $CONTAINER_NAME
                fi
                """
            }
        }

        stage('Run Container') {
            steps {
                sh "docker run -d -p $APP_PORT:$APP_PORT --name $CONTAINER_NAME $IMAGE_NAME:$IMAGE_TAG"
            }
        }
    }
}
