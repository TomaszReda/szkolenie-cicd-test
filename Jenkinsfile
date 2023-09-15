#!groovy

pipeline {
    agent any

    tools {
        maven 'maven-3'
        jdk "jdk-17"
    }

    stages {
        stage('Check Commit Message') {
            steps {
                script {
                    def commitMessage = sh(script: 'git log -1 --pretty=%B', returnStdout: true).trim()

                    if (commitMessage.startsWith('[ci skip]')) {
                        currentBuild.result = 'ABORTED'
                        error('Stopping the build due to [ci skip] in commit message.')
                    }
                }
            }
        }

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
            steps {
                sh 'mvn clean install'
            }
        }
    }

}
