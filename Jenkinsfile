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
                // Use the configured Maven installation name
                sh 'Maven 3.6.3/bin/mvn clean package'
            }
        }
        
        stage('SonarQube Analysis') {
            steps {
                // Assuming SonarQube is configured correctly
                withSonarQubeEnv('http://13.211.153.80:9000') {
                    sh 'Maven 3.6.3/bin/mvn sonar:sonar'
                }
            }
        }
    }
}

