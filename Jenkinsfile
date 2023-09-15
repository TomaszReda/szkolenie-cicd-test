#!groovy

pipeline {
    agent any

    tools {
        maven 'maven-3'
        jdk "jdk-17"
    }

    stages {
        stage('Check Commit Message') {
            when {
                not {
                    changelog '.*ci skip.*'
                }
            }
            steps {
                script {
                    print('aaa')
//                    scmSkip(deleteBuild: false, skipPattern:'.*ci skip.*')
                }
            }
        }
        stage('Cleanup') {
            when {
                not {
                    changelog '.*ci skip.*'
                }
            }
            steps {
                cleanWs()
            }
        }
        stage('Checkout') {
            when {
                not {
                    changelog '.*ci skip.*'
                }
            }
            steps {
                git(url: 'https://github.com/TomaszReda/szkolenie-cicd-jenkins-gitlab-example', branch: 'main')
            }
        }
        stage('Build & Test') {
            when {
                not {
                    changelog '.*ci skip.*'
                }
            }
            steps {
                sh 'mvn clean install'
            }
        }
    }
}