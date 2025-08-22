pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Building...'
      }
    }
    stage('Deploy') {
      steps {
        script {
          echo 'Deploying...'
        }
      }
    }
  }
}
environment {
    BLUE_IMAGE = "nodejs-blue:v1"
    GREEN_IMAGE = "nodejs-green:v1"
  }

stage('Build Blue Image') {
  steps {
    bat 'docker build -t nodejs-blue:v1 ./blue'
  }
}

stage('Build Green Image') {
  steps {
    bat 'docker build -t nodejs-green:v1 ./green'
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
