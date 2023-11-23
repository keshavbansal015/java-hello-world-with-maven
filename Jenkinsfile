pipeline {
    agent any

    environment {
        GCP_CREDENTIALS = credentials('235ba7af-ed73-48bf-a04f-d5510dd873d5')
    }

    tools {
        maven 'maven3'
        jdk 'JDK8'
    }

    stages {
        // stage('Deploy to GCP') {
        //     steps {
        //         // Use the credentials in your steps
        //         withCredentials([file(credentialsId: 'jenkins_secret_id', variable: 'GCP_JSON_KEY')]) {
        //             sh 'gcloud auth activate-service-account --key-file=GCP_JSON_KEY'
        //             // Include any additional GCP specific commands here if needed
        //         }
        //     }
        // }
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
                // sh 'mvn test' // Maven test command
                echo "Test stage completed."
            }
        }
        stage('Deploy') {
            steps {
                echo "Deploying the application"
                // sh 'sudo systemctl stop your-application.service' // Stop the current app
                // sh 'cp target/your-application.jar /path/to/deployment/' // Copy new jar
                // sh 'sudo systemctl start your-application.service' // Start the new app
                sh 'java -cp target/jb-hello-world-maven-0.2.0.jar hello.HelloWorld'
                echo "Deployment completed."
            }
        }
        stage('Monitor') {
            steps {
                // Example of sending a custom metric
                sh 'gcloud monitoring metrics create --metric TEST_METRIC --description "Test of my metric"'

                // Example of writing logs
                sh 'echo "TESTING THE LOG" | gcloud logging write KESHAV'
            }
        }
    }
}
