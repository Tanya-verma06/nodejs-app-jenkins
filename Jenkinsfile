pipeline {

    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm ci'
            }
        }

        stage('Test') {
            steps {
                sh 'npm test'
            }
        }

        stage('Build') {
            steps {
                sh 'node --check app.js'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t nodejs-app-jenkins:latest .'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    docker stop nodejs-app-jenkins || true
                    docker rm nodejs-app-jenkins || true

                    docker run -d \
                        --name nodejs-app-jenkins \
                        -p 3000:3000 \
                        nodejs-app-jenkins:latest
                '''
            }
        }
    }

    post {
        success {
            echo 'CI/CD PIPELINE SUCCESSFUL!'
            echo 'Application deployed on port 3000'
        }

        failure {
            echo 'CI/CD PIPELINE FAILED!'
        }
    }
}
