<<<<<<< HEAD
pipeline {
  agent any

  stages {
    stage('Build') {
      steps {
        echo 'Building Node.js app...'
        sh 'npm install'
      }
    }

    stage('Test') {
      steps {
        echo 'Running tests...'
        sh 'npm test'
      }
    }

    stage('Deploy') {
      steps {
        echo 'Deploying to Kubernetes...'
        sh 'helm upgrade --install nodejs-app ./helm-chart -n blue-green'
      }
    }
  }
}
=======
pipeline { agent any } 
>>>>>>> 13179f3 (Add Helm deployment stage)
