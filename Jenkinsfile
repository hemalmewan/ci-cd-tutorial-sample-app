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

        stage('Build Docker Image') {
        stage('Install Dependencies') {
            steps {
                script {
                    sh 'docker build -t $APP_NAME .'
                }
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    sh 'docker run --rm $APP_NAME pytest tests/'
                }
                sh 'pytest tests'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t flask-ci-cd-demo .'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh 'docker run -d -p 5000:5000 --name flask-app flask-ci-cd-demo'
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
        success {
            echo "Build and tests passed!"
            echo 'Success! App built and tested.'
        }
        failure {
            echo "Build or tests failed!"
            echo 'Build or tests failed.'
        }
    }
}

}
