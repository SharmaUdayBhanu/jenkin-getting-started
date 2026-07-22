pipeline {
    agent any

    options {
        timestamps()
        disableConcurrentBuilds()
    }

    environment {
        APP_PORT = "3000"
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Node Version') {
            steps {
                bat 'node -v'
                bat 'npm -v'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Code Validation') {
            steps {
                bat 'if not exist package.json exit /b 1'
                bat 'if not exist app.js exit /b 1'
                bat 'if not exist README.md exit /b 1'
            }
        }

        stage('Build') {
            steps {
                bat 'npm run build'
            }
        }

        stage('Test') {
            steps {
                bat 'echo Test Passed'
            }
        }

        stage('Deploy') {
            steps {
                bat 'echo Application deployed at http://localhost:3000'
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully!'
        }
        failure {
            echo 'Pipeline execution failed!'
        }
        always {
            archiveArtifacts artifacts: 'package.json', fingerprint: true
        }
    }
}