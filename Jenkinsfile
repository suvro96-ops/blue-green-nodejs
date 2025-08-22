pipeline {
    agent any

    environment {
        IMAGE_NAME = 'nodejs-blue'
        IMAGE_TAG = 'v1'
    }
 stages {
        stage('Build Docker Image') {
            steps {
                bat 'docker build -t my-app .'
            }
        }

        stage('Deploy with Helm') {
            steps {
                bat 'helm upgrade my-app ./chart'
            }
        }

        stage('Switch Traffic') {
            steps {
                echo 'Switching traffic to new deployment...'
            }
        }
    }
}
stage('Smoke Test') {
  steps {
    echo 'Running health checks...'
    // Add curl or kubectl readiness probe here
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
