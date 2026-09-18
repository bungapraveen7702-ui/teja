pipeline{
    agent any 
    stages{
        stage('checkout'){
            steps{
                git branch: 'main', url: 'https://github.com/bungapraveen7702-ui/teja.git'
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
        stage('SonarQube Analysis'){
            steps{
                withSonarQubeEnv('SonarQube-server'){
                    sh 
                    sonar-scanner\
                    -Dsonar.projectkey=SP-Cake-site\
                    -Dsonar.projectName="sp cake & Delight"\
                    -Dsonar.sources=src\
                    -Dsonar.test=src\
                    -Dsonar.test.inclusions="**/*.test.js"\
                    -Dsonar.exclusions="**/*.test.js,**/node_modules/**"\
                    -Dsonar.javascript.lcov.reportpaths=coverage/lcov.info
                }
            }
        }
        
    }
}

