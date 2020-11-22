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
        changed {
            echo "pipeline post changed"
        }

        always {
            echo "pipeline post always"
        }

        success {
            echo "pipeline post success"
        }

        failure {
            echo "Failed"
            mail to: 'abc@xyz.com', subject: 'the pipeline failed.'
        }
    }
}