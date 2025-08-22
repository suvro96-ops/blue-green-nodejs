pipeline {
  agent any
  steps {
    step('Build') {
      script {
        echo 'Building...'
      }
    }
    step('Deploy') {
        script {
          echo 'Deploying...'
        }
      }
    }
  }
environment {
    BLUE_IMAGE = "nodejs-blue:v1"
    GREEN_IMAGE = "nodejs-green:v1"
  }

step('Build Blue Image') {
  script {
    bat 'docker build -t nodejs-blue:v1 ./blue'
  }
}
step('Build Green Image') {
  script {
    bat 'docker build -t nodejs-green:v1 ./green'
  }
}
step('Deploy to Kubernetes') {
        script {
          def targetEnv = (env.BUILD_NUMBER.toInteger() % 2 == 0) ? "blue" : "green"
          echo "Deploying to ${targetEnv} environment..."
          sh "helm upgrade --install nodejs-app-${targetEnv} ./helm-chart -n ${targetEnv}"
        }
      }
    }
  }
