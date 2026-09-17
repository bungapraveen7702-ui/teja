pipeline {
    agent any

    tools {
        nodejs 'node'
    }

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/bungapraveen7702-ui/teja.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('ESLint Analysis') {
            steps {
                sh 'npx eslint src'
            }
        }

        stage('Run Unit Tests') {
            environment {
                CI = 'true'
            }
            steps {
                sh 'npm test -- --coverage --watchAll=false'
            }
        }
    }
}