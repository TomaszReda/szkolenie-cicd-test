pipeline {
    agent any

  tools {
        maven 'maven-3'
        jdk "jdk-17"
    }

    stages {
        stage('Cleanup') {
            steps {
                cleanWs()
            }
        }
        stage('Checkout') {
            steps {
                git(url: 'http://github.com/spring-projects/spring-petclinic.git', branch: 'main')
            }
        }
        stage('Build & Test') {
                steps {
                    sh 'mvn clean test'
                }
                post {
                    always {
                        junit '**/target/surefire-reports/*.xml'
                    }
                    success {
                        slackSend (color: 'good', message: "SUCCESS: Job '${env.BUILD_TAG}' <${env.BUILD_URL}|link> completed successfully.", channel: "#jenkins-tomasz-reda")
                    }
                    failure {
                        slackSend (color: 'danger', message: "FAILURE: Job '${env.BUILD_TAG}' <${env.BUILD_URL}|link> has failed.", channel: "#jenkins-tomasz-reda")
                    }
                    unstable {
                        slackSend (color: 'warning', message: "UNSTABLE: Job '${env.BUILD_TAG}' <${env.BUILD_URL}|link> is unstable.", channel: "#jenkins-tomasz-reda")
                    }
                }
            }
    }

}
