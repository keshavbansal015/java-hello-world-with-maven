pipeline {
    agent any

    tools {
        maven 'maven3'
    }

    stages {
        stage('checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'github access', url: 'https://github.com/keshavbansal015/java-hello-world-with-maven.git']]])
            }
        }
        stage('build') {
            steps {
               sh 'mvn package'
               sh 'mvn compile'
               sh 'mvn install'
            }
        }
        stage('Test') {
            steps {
                echo "Test stage completed."
            }
        }
        stage('Deploy') {
            steps {
                echo "Deploying the application"
                sh 'java -cp target/jb-hello-world-maven-0.2.0.jar hello.HelloWorld'
                echo "Deployment completed."
            }
        }
        stage('Monitor') {
            steps {
                // Example of sending a custom metric
                sh 'gcloud logging write KESHAV "TESTING THE LOG" --severity=INFO'
            }
        }
    }
}
