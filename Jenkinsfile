]pipeline{
    agent any 
    stages{
        stage('checkout'){
            steps{
                checkout scm
            }
        }
        stage('Install Dependencies'){
            steps{
                sh 'npm install'
            }
        }
        stage('ESLint Analysis'){
            steps{
                sh 'npx eslint .'
            }
        }
        stage('Run unit tests'){
            steps{
                sh 'npm test'
            }
        }
        stage('SonarQube Analysis') {
    steps {
        dir('cake') {
            withSonarQubeEnv('SonarQube-Server') {
                sh '''
                    sonar-scanner \
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

