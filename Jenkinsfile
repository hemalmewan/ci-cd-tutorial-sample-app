pipeline {
    agent any

    environment {
        APP_NAME = 'ci-cd-flask-app'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/your-username/ci-cd-tutorial-sample-app.git'
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
    }

    post {
        success {
            echo "Build and tests passed!"
        }
        failure {
            echo "Build or tests failed!"
        }
    }
}
