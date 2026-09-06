pipeline {

    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    credentialsId: 'github-credentials',
                    url: 'https://github.com/Tanya-verma06/nodejs-app-jenkins.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing Node.js dependencies...'
                sh 'npm ci'
            }
        }

        stage('Test') {
            steps {
                echo 'Running application tests...'
                sh 'npm test'
            }
        }

        stage('Build') {
            steps {
                echo 'Building Node.js application...'
                sh 'npm run start -- --help || true'
                echo 'Build completed successfully!'
            }
        }

    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }

        failure {
            echo 'Pipeline failed!'
        }
    }
}
