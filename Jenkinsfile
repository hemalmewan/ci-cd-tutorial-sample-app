pipeline {
    agent any

    environment {
        APP_NAME = 'flask-ci-cd-app'
        DOCKER_BUILDKIT = 1
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/hemalmewan/ci-cd-tutorial-sample-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t $APP_NAME ."
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    // Stop and remove existing container if running (optional)
                    sh "docker rm -f flask-app || true"
                    // Run the app container
                    sh "docker run -d -p 8000:8000 --name flask-app $APP_NAME"
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
        success {
            echo 'App built and deployed successfully.'
        }
        failure {
            echo 'Build or deployment failed.'
        }
    }
}
