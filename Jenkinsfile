pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                script {
                    // Utiliser les identifiants de Jenkins pour le checkout Git
                    checkout([$class: 'GitSCM', branches: [[name: '*/main']], userRemoteConfigs: [[url: 'https://github.com/theoimmersalis/Backend-API-Express.git']]])
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                // Installer les dépendances Node.js
                script {
                    nodejs(nodeJSInstallationName: 'Node 6.x', configId: '<config-file-provider-id>') {
                    sh 'npm config ls'
                    sh 'npm install'
                }
            }
        }

        stage('Build') {
            steps {
                // Construire l'application Node.js
                script {
                    sh 'npm run build'
                }
            }
        }

        stage('Test') {
            steps {
                // Exécuter les tests
                script {
                    sh 'npm test'
                }
            }
        }

        stage('Deploy') {
            steps {
                // Déployer l'application (adapter selon vos besoins)
                script {
                    // Exemple : Déployer sur un serveur distant
                    sh 'scp -r dist/ utilisateur@serveur:/chemin/vers/deploy'
                }
            }
        }
    }

    post {
        success {
            // Actions à effectuer en cas de succès du pipeline
            echo 'Le pipeline a réussi!'
        }
        failure {
            // Actions à effectuer en cas d'échec du pipeline
            echo 'Le pipeline a échoué. Veuillez vérifier les logs.'
        }
    }
}
