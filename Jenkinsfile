pipeline {
    agent any

    environment {
        IMAGE_NAME = "todo-app"
        CONTAINER_NAME = "todo-container"
    }

    stages {

        stage('Clone Repo') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Dipesh-Bhadane/Node-app-CICD.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh '''
                docker stop $CONTAINER_NAME || true
                docker rm $CONTAINER_NAME || true
                '''
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker run -d \
                --name $CONTAINER_NAME \
                -p 8000:8000 \
                $IMAGE_NAME
                '''
            }
        }
    }

    post {
        success {
            echo "Deployment Successful 🚀"
        }
    }
}
