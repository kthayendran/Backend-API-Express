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
        stage('Push') {
                    steps {
                        withCredentials([usernamePassword(credentialsId: 'docker-credential', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                            sh 'echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin'
                            sh 'docker tag backend-api-express kthayendran/backend-api:latest'
                            sh 'docker push kthayendran/backend-api:latest'
                        }
                    }
                }
    }
}