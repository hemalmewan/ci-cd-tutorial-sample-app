pipeline {
    agent any

    environment {
        APP_NAME = 'ci-cd-flask-app'
        DOCKER_BUILDKIT = 1
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/hemalmewan/ci-cd-tutorial-sample-app.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    sh 'pip install -r requirements.txt'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t $APP_NAME .'
                }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    sh 'docker run --rm $APP_NAME pytest tests/'
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    sh 'docker run -d -p 5000:5000 --name flask-app $APP_NAME'
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
        success {
            echo 'Build and tests passed!'
        }
        failure {
            echo 'Build or tests failed!'
        }
    }
}
