pipeline {
    agent any

    tools {
        jdk "jdk-17"
        maven "maven-3"
    }


    triggers {
        cron('*/1 * * * *')
    }

    stages {
        stage('Clean workspace') {
            steps {
                cleanWs()
            }
        }

        stage('Fetch repo') {
            steps {
                git branch: 'main', url: 'https://github.com/dc-michal-michalski/szkolenie-cicd-jenkins-gitlab-example.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean verify'
                junit '**/target/**/*.xml'
            }
        }
    }
    post {
        success {
            slackSend message: "Success $BUILD_TAG"
        }
        unstable {
            slackSend message: "Unstable $BUILD_TAG"
        }
        failure {
            slackSend message: "failure $BUILD_TAG"
        }
    }
}
