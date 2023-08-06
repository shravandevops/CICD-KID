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
                    sh '/usr/bin/mvn sonar:sonar' // Use the correct path to Maven executable
                }
            }
        }
    }
}

