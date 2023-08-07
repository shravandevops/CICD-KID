pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh '/usr/bin/mvn clean package' // Use the correct path to Maven executable
            }
        }

        stage('SonarQube Analysis') {
            steps {
                // Assuming SonarQube is configured correctly
                withSonarQubeEnv('http://13.211.153.80:9000') {
                    sh '/usr/bin/mvn sonarqube:sonarqube' // Use the correct path to Maven executable
                }
            }
        }
        stage('Build and Push Docker Image') {
    environment {
        DOCKER_REGISTRY_URL = "docker.io"
        DOCKER_IMAGE = "shravandevops/java-demo:${BUILD_NUMBER}"
        DOCKER_CREDENTIALS = credentials('docker-cred')

    }
    steps {
        script {
            // Build Docker image
            sh "docker build -t ${DOCKER_IMAGE} ."

            // Authenticate with Docker registry
            withDockerRegistry(credentialsId: 'docker-cred', url: "${DOCKER_REGISTRY_URL}") {
                // Push Docker image to the registry
                sh "docker push ${DOCKER_IMAGE}"
            }
        }
    }
}

    }
}

