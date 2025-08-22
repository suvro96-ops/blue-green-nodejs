pipeline {
    agent any

    environment {
        IMAGE_NAME = 'nodejs-blue'
        IMAGE_TAG = 'v1'
    }
    stage('Build Docker Image') {
  steps {
    script {
      def targetEnv = (env.BUILD_NUMBER.toInteger() % 2 == 0) ? "blue" : "green"
      def imageTag = "nodejs-${targetEnv}:v${env.BUILD_NUMBER}"
      echo "Building Docker image for ${targetEnv} → ${imageTag}"
      bat "docker build -t ${imageTag} ./${targetEnv}"
    }
  }
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
