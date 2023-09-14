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
                git(url: 'https://github.com/TomaszReda/szkolenie-cicd-jenkins-gitlab-example', branch: 'main')
            }
        }
        stage('Build & Test') {
             sh 'mvn clean test'
        }
    }

}
