pipeline {
  agent any

  environment {
    BLUE_IMAGE = "nodejs-blue:v1"
    GREEN_IMAGE = "nodejs-green:v1"
  }

  stages {
    stage('Build Blue Image') {
      steps {
        echo 'Building Blue Docker Image...'
        sh 'docker build -t $BLUE_IMAGE ./blue'
      }
    }

    stage('Build Green Image') {
      steps {
        echo 'Building Green Docker Image...'
        sh 'docker build -t $GREEN_IMAGE ./green'
      }
    }

    stage('Deploy to Kubernetes') {
      steps {
        script {
          def targetEnv = (env.BUILD_NUMBER.toInteger() % 2 == 0) ? "blue" : "green"
          echo "Deploying to ${targetEnv} environment..."
          sh "helm upgrade --install nodejs-app-${targetEnv} ./helm-chart -n ${targetEnv}"
        }
      }
    }
  }
}
