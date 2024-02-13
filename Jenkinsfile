pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'mon_project_image'
        CONTAINER_NAME = 'mon_container_sqlite'
        DOCKER_CREDENTIALS_ID = 'mes_credentials_docker'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Test') {
            steps {
                sh 'echo "Lancer les tests ici..."'
                // Insérez les commandes pour exécuter vos tests
            }
        }

        stage('Build') {
            steps {
                script {
                    // Étape de compilation avec Maven
                    sh 'mvn clean install'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Construction de l'image Docker avec le tag "latest"
                    docker.build("${DOCKER_IMAGE}:latest")
                }
            }
        }

        stage('Deploy Docker Container') {
            steps {
                script {
                    // Suppression de l'ancien conteneur si il existe
                    sh "docker rm -f ${CONTAINER_NAME} || true"

                    // Exécution du nouveau conteneur
                    sh "docker run -d -p 5432:5432 --name ${CONTAINER_NAME} -e POSTGRES_PASSWORD=project_2024 ${DOCKER_IMAGE}:latest"
                }
            }
        }
    }

    post {
        always {
            sh 'echo "Nettoyage post-build..."'
            // Insérez ici les commandes pour le nettoyage post-build si nécessaire
        }
    }
}
