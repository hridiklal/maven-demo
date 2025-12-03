pipeline {
    agent any

    tools {
        maven 'Maven-3.9'   // Use the name you set in Jenkins Global Tool Configuration
    }

    stages {

        stage('Checkout') {
            steps {
                echo "Fetching source code..."
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo "Building the application without tests..."
                bat 'mvn clean install -DskipTests'
            }
        }

        stage('Package') {
            steps {
                echo "Packaging application..."
                bat 'mvn package -DskipTests'
            }
            post {
                success {
                    archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
                }
            }
        }
    }

    post {
        success {
            echo "Build completed successfully."
        }
        failure {
            echo "Build failed."
        }
    }
}
