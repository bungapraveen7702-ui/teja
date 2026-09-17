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
            environment {
                CI = 'true'
            }
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
                            -Dsonar.projectName="SP Cakes & Delight" \
                            -Dsonar.sources=src \
                            -Dsonar.tests=src \
                            -Dsonar.test.inclusions="**/*.test.js" \
                            -Dsonar.exclusions="**/*.test.js,**/node_modules/**" \
                            -Dsonar.javascript.lcov.reportPaths=coverage/lcov.info
                        '''
                    }
                }
            }
        }
    }
}