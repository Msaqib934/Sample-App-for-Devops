pipeline {
    agent any
    environment {
        VERSION = "${env.BUILD_ID}"
    }
    tools {
        maven 'maven3'
    }
    stages {
        stage('mvn clean') {
            steps {
                sh "mvn clean install"
            }
        }
        stage('push') {
            steps {
                script {
                    withCredentials([string(credentialsId: 'docker_pass', variable: 'docker')]) {
                        sh '''
                        docker build . -t msaqib934/devops-training:${VERSION}
                        docker push msaqib934/devops-training:${VERSION}
                        docker rmi msaqib934/devops-training:${VERSION}
                        '''
                    }
                }
            }
        }
    }
}
