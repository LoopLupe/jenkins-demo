pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
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