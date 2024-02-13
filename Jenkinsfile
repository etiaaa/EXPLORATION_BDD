pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build and Deploy') {
            steps {
                script {
                    // Étape de compilation (ajuster selon votre projet)
                    sh 'mvn clean install'

                    // Étape de construction de l'image Docker
                    docker.build("Project_Image-Docker:latest")

                    // Étape de déploiement du conteneur Docker
                    sh 'docker run -d -p 5432:5432 --name sqlite-container -e POSTGRES_PASSWORD=project_2024 Project_Image-Docker:latest'
                }
            }
        }
    }
}
