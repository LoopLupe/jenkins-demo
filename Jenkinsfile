pipeline {
    agent any

    tools {
        maven 'mvn-3.6.0'
    }

    stages {
        stage('Build') {
            steps {
                sh "mvn clean package spring-boot:repackage"
                sh "printenv"
                echo 'Hello World'
            }
        }
    }
    
    post {
        failure {
            echo "Failed"
        }
    }
}