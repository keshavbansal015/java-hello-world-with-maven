pipeline {
    agent any

    environment {
        GCP_CREDENTIALS = credentials('8fd29018-8b09-409b-9ea9-5651597897de')
    }

    tools {
        maven 'maven'
        jdk 'java'
    }

    stages {
        stage('Deploy to GCP') {
            steps {
                // Use the credentials in your steps
                withCredentials([googleComputeServiceAccount(credentialsId: '8fd29018-8b09-409b-9ea9-5651597897de', jsonKeyVariable: 'GCP_CREDENTIALS')]) {
                    sh 'gcloud auth activate-service-account --key-file=$GCP_CREDENTIALS'
                    // Include any additional GCP specific commands here if needed
                }
            }
        }
        stage('checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'github access', url: 'https://github.com/keshavbansal015/java-hello-world-with-maven.git']]])
            }
        }
        stage('build') {
            steps {
               sh 'mvn package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test' // Maven test command
                echo "Test stage completed."
            }
        }
        stage('Deploy') {
            steps {
                echo "Deploying the application"
                // sh 'sudo systemctl stop your-application.service' // Stop the current app
                // sh 'cp target/your-application.jar /path/to/deployment/' // Copy new jar
                // sh 'sudo systemctl start your-application.service' // Start the new app
                echo "Deployment completed."
            }
        }
    }
}
