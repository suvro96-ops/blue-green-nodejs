pipeline {
  agent any

  environment {
    BLUE_IMAGE = "blue-app:latest"
    GREEN_IMAGE = "green-app:latest"
  }

  stages {
    stage('Build Blue Image') {
      steps {
        echo "Building Blue Docker image..."
        sh 'docker build -t $BLUE_IMAGE ./blue'
      }
    }

    stage('Deploy Blue to Kubernetes') {
      steps {
        echo "Deploying Blue version to cluster..."
        sh 'kubectl apply -f k8s/blue-deployment.yaml'
        sh 'kubectl apply -f k8s/service.yaml'
      }
    }

    stage('Build Green Image') {
      steps {
        echo "Building Green Docker image..."
        sh 'docker build -t $GREEN_IMAGE ./green'
      }
    }

    stage('Deploy Green to Kubernetes') {
      steps {
        echo "Deploying Green version to cluster..."
        sh 'kubectl apply -f k8s/green-deployment.yaml'
      }
    }

    stage('Switch Traffic to Green') {
      steps {
        echo "Switching service selector to Green..."
        sh '''kubectl patch svc nodejs-service \
          -p '{"spec":{"selector":{"app":"green"}}}' '''
      }
    }
  }

  post {
    success {
      echo "✅ Blue-Green deployment completed successfully!"
    }
    failure {
      echo "❌ Deployment failed. Check logs for details."
    }
  }
}
