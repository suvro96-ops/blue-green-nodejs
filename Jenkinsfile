pipeline {
    agent any

    environment {
        GITHUB_TOKEN = credentials('github-token')
    }

    stages {
        stage('Clone Repo') {
            steps {
                git url: 'https://github.com/your-username/your-repo.git',
                    credentialsId: 'github-token'
            }
        }
    }
}
