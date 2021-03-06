pipeline {
    agent any

    tools {
        maven 'mvn-3.6.0'
    }

    // Valid option types: [authorizationMatrix, buildDiscarder, catchError, checkoutToSubdirectory, disableConcurrentBuilds, disableResume, durabilityHint, lock, overrideIndexTriggers, parallelsAlwaysFailFast, preserveStashes, quietPeriod, rateLimitBuilds, retry, script, skipDefaultCheckout, skipStagesAfterUnstable, timeout, timestamps, waitUntil, warnError, withContext, withCredentials, withEnv, wrap, ws]
    options {
        buildDiscarder(logRotator(numToKeepStr: '10'))
        // checkoutToSubdiretory('subDir')
        disableConcurrentBuilds()
        // newContainerPerStage()
        retry(2)
        timeout(time: 60, unit: 'SECONDS')
    }

    stages {
        stage('stash') {
            agent {label "master"}
            steps {
                writeFile file: "a.txt", text: "${BUILD_NUMBER}"
                stash(name: "abc", includes: "a.txt")
            }
        }

        stage('unstash') {
            agent {label "master"}
            steps {
                script {
                    unstash("abc")
                    def content = readFile(file: "a.txt", encoding: "UTF-8")
                    echo "${content}"
                }

            }
        }

        stage('Build') {
            steps {
                script {
                    def browsers = ['chrome', 'firefox']
                    for (int i =0; i < browsers.size(); ++i) {
                        echo "testing the ${browsers[i]} browser"
                    }

                    def pwd = pwd()
                    echo "${pwd}"

                    writeFile(file: "base64File", text: "amVua2lucyBib29r", encoding: "Base64")
                    def content = readFile(file: "base64File", encoding: "UTF-8")
                    echo "${content}"
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
            // mail to: 'abc@xyz.com', subject: 'the pipeline failed.', body: 'hello world'
        }

        cleanup {
            echo "pipeline post cleanup"
        }
    }
}