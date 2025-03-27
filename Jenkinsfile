pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/main']],
                    userRemoteConfigs: [[
                        url: 'https://github.com/kthayendran/Backend-API-Express',
                        credentialsId: 'github-credentials'
                    ]]
                ])
            }
        }
        stage('Build') {
            steps {
                sh 'docker build -t backend-api-express .'
            }
        }
        stage('Test') {
            steps {
                sh 'npm install --save-dev mocha'
                sh 'npm run test'
            }
        }
    }
}