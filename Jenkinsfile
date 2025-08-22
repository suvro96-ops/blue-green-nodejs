pipeline {
    agent any

    environment {
        IMAGE_NAME = 'nodejs-blue'
        IMAGE_TAG = 'v1'
    }

    stages {
        stage('Build Blue') {
            steps {
                bat "docker build -t ${IMAGE_NAME}:${IMAGE_TAG} ./blue"
            }
        }

        stage('Build Green') {
            steps {
                bat "docker build -t nodejs-green:v1 ./green"
            }
        }
    }
}
