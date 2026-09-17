pipeline {
    agent any

    tools {
        nodejs 'node'
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                dir('cake') {
                    sh 'npm install'
                }
            }
        }

        stage('ESLint Analysis') {
            steps {
                dir('cake') {
                    sh 'npx eslint src'
                }
            }
        }

        stage('Run Unit Tests') {
            steps {
                dir('cake') {
                    sh 'npm test'
                }
            }
        }

        stage('SonarQube Analysis') {
            steps {
                dir('cake') {
                    withSonarQubeEnv('SonarQube-Server') {
                        sh '''
                            npx sonarqube-scanner \
                            -Dsonar.projectKey=SP-Cakes-Site \
                            -Dsonar.sources=src
                        '''
                    }
                }
            }
        }
    }
}