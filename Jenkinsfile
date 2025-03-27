pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/main']],
                    userRemoteConfigs: [[
                        url: 'VotreDépotGit',
                        credentialsId: 'github-credentials'
                    ]]
                ])
            }
        }
        // stage('Build') {
        //     steps {
        //         // TODO
        //     }
        // }
        // stage('Test') {
        //     steps {
        //         // TODO
        //     }
        // }
    }
}