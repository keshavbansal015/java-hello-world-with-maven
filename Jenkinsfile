pipeline{
    agent any

    tools {
         maven 'maven'
         jdk 'java'
    }

    stages{
        stage('checkout'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'github access', url: 'https://github.com/keshavbansal015/java-hello-world-with-maven.git']]])
            }
        }
        stage('build'){
            steps{
               bat 'mvn package'
            }
        }
        // stage('Test') {
        //     steps {
        //         // Add test commands here, for instance:
        //         sh 'mvn test' // Maven test command
        //     }
        // }
        
        // stage('Deploy') {
        //     steps {
        //         // Add deployment commands here, for instance:
        //         sh 'scp target/your-application.jar user@your-server:/path/to/deployment/' // Example deployment command
        //     }
        // }
    }
}
