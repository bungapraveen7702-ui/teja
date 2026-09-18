pipeline {
    agent any

    stages {
        stage('checkout') {
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
                sh 'npx eslint .'
            }
        }

        stage('Run unit tests') {
            steps {
                sh 'npm test'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube-server') {
                    script {
                        def scannerHome = tool 'SonarScanner'

                        withCredentials([string(credentialsId: 'sonar-token', variable: 'SONAR_TOKEN')]) {
                            withEnv(["PATH+SONAR=${scannerHome}/bin"]) {
                                sh '''
                                    sonar-scanner \
                                      -Dsonar.projectKey=SP-Cake-site \
                                      -Dsonar.projectName="sp cake & Delight" \
                                      -Dsonar.sources=src \
                                      -Dsonar.tests=src \
                                      -Dsonar.test.inclusions="**/*.test.js" \
                                      -Dsonar.exclusions="**/*.test.js,**/node_modules/**" \
                                      -Dsonar.javascript.lcov.reportPaths=coverage/lcov.info \
                                      -Dsonar.token=$SONAR_TOKEN
                                '''
                            }
                        }
                    }
                    stage('SonarQube Quality Gate'){
                        steps{
                            timeout(time:5, unit:'MINUTES'){
                                waitForQualityGate abortPipeline:true
                            }
                        }
                    }
                }
            }
        }
    }
}