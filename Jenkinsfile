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
        
    }
}

