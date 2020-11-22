pipeline {
    agent any

    tools {
        maven 'mvn-3.6.0'
    }

    options {
        buildDiscarder(logRotator(numToKeepStr: '10'))
        checkoutToSubdiretory('subDir')
        disableConcurrentBuilds()
        newContainerPerStage()
        retry(4)
        timeout(time: 60, unit: 'SECONDS')
    }

    stages {
        stage('Build') {
            steps {
                script {
                    def browsers = ['chrome', 'firefox']
                    for (int i =0; i < browsers.size(), ++i) {
                        echo "testing the ${broswers[i]} browser"
                    }
                }
                sh 'mvn -v'
                // sh "mvn clean package spring-boot:repackage"
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
            mail to: 'abc@xyz.com', subject: 'the pipeline failed.', body: 'hello world'
        }

        cleanup {
            echo "pipeline post cleanup"
        }
    }
}