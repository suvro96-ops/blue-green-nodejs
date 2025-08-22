pipeline {
  agent any

  environment {
    BLUE_IMAGE = "nodejs-blue:v1"
    GREEN_IMAGE = "nodejs-green:v1"
    HELM_CHART_PATH = "./helm-chart"
  }

  stages {
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

    stage('Deploy with Helm') {
      steps {
        script {
          def targetEnv = (env.BUILD_NUMBER.toInteger() % 2 == 0) ? "blue" : "green"
          echo "Deploying to Kubernetes namespace: ${targetEnv}"

          bat "helm upgrade --install nodejs-app-${targetEnv} ${HELM_CHART_PATH} -n ${targetEnv} --create-namespace"
        }
      }
    }

    stage('Smoke Test') {
      steps {
        echo 'Running basic health checks...'
        // Add curl or kubectl checks here
      }
    }

    stage('Switch Traffic') {
      steps {
        script {
          def targetEnv = (env.BUILD_NUMBER.toInteger() % 2 == 0) ? "blue" : "green"
          echo "Switching live traffic to ${targetEnv} environment..."
          // You can patch Kubernetes service selector or use Ingress routing here
        }
      }
    }
  }
}
